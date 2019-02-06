# Main repository

This is the main repository, which consists of submodules.

## How to go about submodules

Step 1: Create an independent git repository named `submodule_one`.


Step 2: Add submodule to your `main_repository`, by

	cd main_repository

	## initialize submodule in the main_repository
	git submodule init

	## add submodule_one as a remote to the main_repository
	git submodule add git@github.com:nturaga/submodule_one submodule_one

Step 3: Inspect `.gitmodules`. This shows the name of the submodule
and the remote location in github.

	$ cat .gitmodules

	[submodule "submodule_one"]
		path = submodule_one
		url = git@github.com:nturaga/submodule_one

Step 4: Commit the submodule to the `main_repository`.

	git commit -m "Add submodule_one"
