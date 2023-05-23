# Geological Interpretor Proof of Concept
Minimal working code to illustrate a Geological Interpretor based on formal knowledge


# Development advices

## Notebook management
If you intend to commit changes to the notebooks versionned in this project,
please edit your environnement in the following way beforehand to avoid versionning
local information and execution count.

1. Install **jq** if needed (from https://stedolan.github.io/jq/) making it accessible into your *path*
2. Edit the *config* file in the *.git* folder in the repository directory
3. Add the following piece of code:

        [filter "nbstrip_full"]
        clean = "jq --indent 1 \
            '(.cells[] | select(has(\"outputs\")) | .outputs) = []  \
            | (.cells[] | select(has(\"execution_count\")) | .execution_count) = null  \
            | .metadata = {\"language_info\": {\"name\": \"python\", \"pygments_lexer\": \"ipython3\"}} \
            | .cells[].metadata = {} \
            '"
        smudge = cat
        required = true

4. Create a *.gitattributes* file in the main folder of the repository (if not already there) and add in

        *.ipynb filter=nbstrip_full

