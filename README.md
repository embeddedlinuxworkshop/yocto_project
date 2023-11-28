Layer 1: meta-custom1
Layer Structure:

Create a directory for your layer, for example, meta-custom1.
Inside the layer directory, create a conf subdirectory and add a layer.conf file.
plaintext
Copy code
meta-custom1/
├── conf
│   └── layer.conf
The layer.conf file might look like this:
conf
Copy code
# meta-custom1/conf/layer.conf
BBPATH .= ":${LAYERDIR}"
BBFILES += "${LAYERDIR}/recipes-*/*/*.bb ${LAYERDIR}/recipes-*/*/*.bbappend"
Recipe in meta-custom1:

Create a recipe directory, for example, recipes-example inside meta-custom1.
Inside the recipes-example directory, add a basic recipe, e.g., example-recipe.bb:
plaintext
Copy code
meta-custom1/
├── recipes-example
│   └── example-recipe
│       └── example-recipe.bb
The example-recipe.bb file might contain:
conf
Copy code
SUMMARY = "Example Recipe"
DESCRIPTION = "An example recipe for Yocto"
LICENSE = "MIT"

SRC_URI = "file://example_file.txt"

do_compile() {
    # Compilation steps
}

do_install() {
    # Installation steps
}
Layer 2: meta-custom2
Layer Structure:

Create a directory for your second layer, for example, meta-custom2.
Similar to meta-custom1, create a conf subdirectory and add a layer.conf file.
plaintext
Copy code
meta-custom2/
├── conf
│   └── layer.conf
The layer.conf file for meta-custom2 might look like:
conf
Copy code
# meta-custom2/conf/layer.conf
BBPATH .= ":${LAYERDIR}"
BBFILES += "${LAYERDIR}/recipes-*/*/*.bb ${LAYERDIR}/recipes-*/*/*.bbappend"
Recipe in meta-custom2 with Dependency:

Create a recipe directory, for example, recipes-dependent inside meta-custom2.
Inside the recipes-dependent directory, add a recipe, e.g., dependent-recipe.bb:
plaintext
Copy code
meta-custom2/
├── recipes-dependent
│   └── dependent-recipe
│       └── dependent-recipe.bb
The dependent-recipe.bb file might contain:
conf
Copy code
SUMMARY = "Dependent Recipe"
DESCRIPTION = "A recipe with dependency on example recipe"
LICENSE = "GPLv3"

DEPENDS += "example-recipe"

do_compile() {
    # Compilation steps
}

do_install() {
    # Installation steps
}
Note the DEPENDS += "example-recipe" line, indicating the dependency on the example-recipe from meta-custom1.
Building with Yocto Project:
Make sure both layers are sourced in your Yocto build environment, for example, in your bblayers.conf.

Build the image using the Yocto build command:

bash
Copy code
bitbake core-image-minimal
