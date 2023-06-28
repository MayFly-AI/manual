## sensorleap_manual

Instructions below are from [github](https://docs.github.com/en/pages/setting-up-a-github-pages-site-with-jekyll/testing-your-github-pages-site-locally-with-jekyll)

### Installation of jekyll
Install jekyll on Ubuntu (steps copied from [jekyll](https://jekyllrb.com/docs/installation/ubuntu/))

```bash
sudo apt-get install ruby-full build-essential zlib1g-dev
```

Avoid installing RubyGems packages (called gems) as the root user. Instead, set up a gem installation directory for your user account. The following commands will add environment variables to your ~/.bashrc file to configure the gem installation path:

```bash
echo '# Install Ruby Gems to ~/gems' >> ~/.bashrc
echo 'export GEM_HOME="$HOME/gems"' >> ~/.bashrc
echo 'export PATH="$HOME/gems/bin:$PATH"' >> ~/.bashrc
source ~/.bashrc
```

Finally, install Jekyll and Bundler:

```bash
gem install jekyll bundler
```

Navigate to this folder and run
```bash
bundle install .
```

You probably also need this one to make it work:
```bash
bundle add webrick
```

### Run jekyll locally to test site before pushing changes to github
```bash
bundle exec jekyll serve
```





