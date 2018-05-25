# blog.vertigion.com

This is the source for [my blog](http://blog.vertigion.com), hosted by [GitHub Pages](https://pages.github.com/).

## Theme

[Flexible-Jekyll](https://github.com/artemsheludko/flexible-jekyll)

## Notes

### Setup Dev Env

**Setup:** [How to Set Up a Jekyll Development Site on Ubuntu 16.04](https://www.digitalocean.com/community/tutorials/how-to-set-up-a-jekyll-development-site-on-ubuntu-16-04)

- Setup in WLS Ubuntu.
- Didn't open firewall.
- [Nokogiri requires a few more `apt` packages.](http://www.nokogiri.org/tutorials/installing_nokogiri.html#install_with_included_libraries__recommended_)
  - At the time of this writing: `sudo apt-get install build-essential patch ruby-dev zlib1g-dev liblzma-dev`

Then just need to `cd` into this git repo and run the dev server:

```bash
cd vertigoray.github.io
jekyll serve
```

For simplicity later, I made a bash script in WLS's home: `~/jekyll_serve_vertigoray.github.io.sh`.