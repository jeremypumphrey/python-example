# Python example with version locking + SHA–based integrity
## To reduce project supply-chain risk (e.g., registry compromises like the recent Shai-Hulud incident)

### Example using pip-tools
Install requirements:  
`brew install pip-tools` easiest for mac  
  
1) Use Broad dependencies in `requirements.in` only pinned to Major versions using `~=`. Human editable
>  numpy~=2.0  
>  django~=6.0  

2) Run `pip-compile --output-file=requirements.txt --generate-hashes requirements.in` to create `requirements.txt` with specific version locks and SHA package validation. Never edit manually.  
> numpy==2.3.5 \  
>    --hash=sha256:00dc4e846108a382c5869e77c6ed514394bdeb3403461d25a829711041217d5b   

3) Run `pip-audit --requirement requirements.txt --require-hashes --fix` to ensure you aren't locked to known vulnerable packages  

4) Commit the `requirements.txt` file
 
5) In CI/CD pipelines run `pip install --require-hashes -r requirements.txt` rather than `pip install` to do a clean install using only versions (SHA based) and depenedencies from the lockfile

  
### Example using poetry
See https://github.com/jeremypumphrey/python-poetry-example
