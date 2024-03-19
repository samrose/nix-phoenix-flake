# Nix Flake Phoenix Example


You can edit the flake.nix file, and modify `basePackages` in the `devShell` section, set env vars in a `.env` file, and then run `nix develop` 

(the current example bootstraps up a whole posgresql db server and so requires the env vars seen in `hooks` to be set)

If all env vars are set, then supporting services (just postgres in this case) can be run with `overmind start -D` which uses the `Procfile` for local development.


In development shell context, all of the mix deps are installed into gitignored .nix-mix and .nix-hex, so that you can maintain multiple dev envs with unique deps, versions of elixir and postgres etc on one machine.

Once you run `nix develop` you should also run

```
(nix:nix-shell-env) sam@dev:~/phoenix_nix_flake_example$ mix archive.install hex phx_new
Resolving Hex dependencies...
Resolution completed in 0.009s
New:
  phx_new 1.7.11
* Getting phx_new (Hex package)
All dependencies are up to date
Compiling 11 files (.ex)
Generated phx_new app
Generated archive "phx_new-1.7.11.ez" with MIX_ENV=prod
Are you sure you want to install "phx_new-1.7.11.ez"? [Yn] y
* creating /home/sam/phoenix_nix_flake_example/.nix-mix/archives/phx_new-1.7.11
```


now you can just run the phoenix as normal in the dev shell with `mix -S iex phx.server`


