# Crate removal procedure

*status 2019-06-13: this document is incomplete and unvetted. We anticipate to be receiving guidelines from Mozilla Legal in the near future. If this notice is still here on 2019-09-13, please file an issue on this repo to ping for updated status.*

If we get a DMCA takedown notice, here's what needs to happen:

## Remove relevant version(s) and/or entire crates from crates.io

* Remove it from the database:

      heroku run -- cargo run --bin delete-crate crate-name
	
  or

      heroku run -- cargo run --bin delete-version crate-name version-number

* Invalidate the CloudFront cache – remove both the relevant readme and crate files. If in doubt, invalidate `/*` to flush everything.

## Remove relevant version(s) and/or entire crates from docs.rs

The docs.rs codebase doesn't currently have a builtin way to remove the
already-generated docs, so the current approach when a DMCA arrives is to
prevent users accessing the docs at the nginx level. The people who currently
have permissions to access the server are:

* rustdoc team:
  * [@onur](https://github.com/onur)
  * [@QuietMisdreavus](https://github.com/QuietMisdreavus)
* infra team:
  * [@Mark-Simulacrum](https://github.com/Mark-Simulacrum)
  * [@pietroalbini](https://github.com/pietroalbini)
* People with 1password access

One of these people needs to log into the `docsrs.infra.rust-lang.org` machine through the bastion and add
this snippet to `/home/ubuntu/conf/docs.rs.nginx.conf`:

```nginx
		location /CRATENAME {
			return 410;
		}
		location /crate/CRATENAME {
			return 410;
		}
```

Then reload the nginx configuration:

```
$ sudo systemctl reload nginx
```
