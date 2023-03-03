# Interface Design Talking Points 

## Should user edit `flake.nix` manually?

**Goal**: The user should not have to edit `flake.nix`, ever.

**Problem**: What if they want to add a flake input?

**Solution**: Include *all* dependencies in the `devx` flake, and make them avaialble in `devx.inputs`.

**Pros**: We have full control over the nix dependency graph. Any change to it will be picked up automatically by all users of `devx` the moment they run `nix flake lock --update-input devx`.

**Cons**: The user will have to rely on us to update/add the flake inputs.  
  What if they need a new input (or a new version of an existing input) to quickly try something out?

  **Solution**: provide escape patch, i.e. let the user add the inputs to the flake like usual, and make it available in
  `devx.inputs` (NOTE: ensure that a meaningful error message/warning is returned on input clash/override)
