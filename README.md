# Deploying a Static Site on Netlify using Shodo SSG

1. Create your [Shodo SSG](https://github.com/ryanmphill/shodo-static-gen) project

2. Grab the latest commit hash from the [Shodo Repository](https://github.com/ryanmphill/shodo-static-gen) and add the following dependency under `[packages]` in the `pipfile`:

```python
[packages]
shodo_ssg = {git = "https://github.com/ryanmphill/shodo-static-gen", ref = "<latest-commit-hash-goes-here>"}
```

3. Now generate the lock file. If using pipenv: `pipenv lock`, then go ahead and verify the package is installable with the command `pipenv sync`. 

4. Create a new repository on GitHub and push the Shodo project up to it

5. Now, we have everything we will need to build and deploy the static site on Netlify. We will have to make a few specifications since Netlify won't be able to autodetect everything about the build configuration

6. Choose "Add new site" on Netlify, and select the repository with your site

7. For the `build command`, specify `python site_builder.py`

8. For the `publish directory`, specify `dist`

9. Luckily, Netlify supports Python and will be able to automatically install dependencies from the pipfile. The only extra step we need to take is to change the default python version from 3.8 to 3.9. To do this, go to the environment variables section and add `PYTHON_VERSION` for the variable name, and `3.9` for the value.

10. Now click to deploy the site. After around a minute, verify that the build was successful, and you should be able to view the deployed site!