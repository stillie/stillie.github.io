---
title: Deploy a Jekyll site using FTP using GitHub Actions
date: 2023-02-04
categories: [Development]
tags: [github-actions,jekyll,ftp,yml,yaml]
---

I recently was figuring out the best way to automatically deploy my website using GitHub Actions and found that it can be done using FTP to my website host.

The best way I found was to use the following YAML file:

```yaml
name: Build & Upload Site
# Run on pushes to the main branch
on: 
  push:
    branches:
      - main
jobs:
  build:
    runs-on: ubuntu-latest
    steps:
    - uses: actions/checkout@v2
    - uses: actions/setup-ruby@v1
      with:
        ruby-version: '3.1.3'
    # Install the gems in the gemfile & install ncftp
    - name: Setup Environment.
      run: |
        bundle install
        sudo apt-get install -y ncftp
    
    # Build the site
    - name: Build Site with Jekyll.
      run: JEKYLL_ENV=production bundle exec jekyll build
    
    # Looks kind of complicated but just uploads the content of _site folder to the ftp server. It does not upload the _site folder itself.
    - name: Upload site to FTP.
      env: 
        ftp_location: ${{ secrets.FTP_LOCATION }} # Pass in required secrets.
        ftp_username: ${{ secrets.FTP_USERNAME }} #someawesomeftpusername
        ftp_password: ${{ secrets.FTP_PASSWORD }} # somesuperstrongpassword
        ftp_folder: ${{ secrets.FTP_FOLDER }} # /public_html
      run: |
        ncftpput -R -v -u "$ftp_username" -p "$ftp_password" $ftp_location $ftp_folder _site/* 
```

If you would like to use the above YAML you will need to create 4 Secrets in Github:

- `FTP_LOCATION` - The Server address aka `example.com`
- `FTP_USERNAME` - Your FTP Username
- `FTP_PASSWORD` - Your FTP Password
- `FTP_FOLDER` - The folder where the Files must go to in the destination. If you don't want to specify a folder because the user goes directly to the correct folder, just use `/`

One side note is the you need to specify the folder that contains the generated production data. In the last line of the file you need to change `_site/*` to what ever the folder is that contains the generated site files from Jekyll.

## Links for more information
* [Jekyll](https://jekyllrb.com) - A Static site generator
* [ncftpput](https://www.ncftp.com/ncftp/doc/ncftpput.html) - FTP Client used to upload the content to the server

