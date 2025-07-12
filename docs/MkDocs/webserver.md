# Serving/Deploying Mkdocs

## How to serve Mkdocs

1. Once your site/files are ready to be served, run the following command:

    ```
    mkdocs build
    ```

2. The 'site' folder will be created/updated.

3. Connect to the server via FTP and copy the contents of the 'site' folder to the /var/www directory

## How to deploy Mkdocs with GitHub Pages

1. Once your site/files are ready to be deployed, run the following command:

    ```
    mkdocs gh-deploy --force
    ```
