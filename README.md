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


## How to update submodules

Use the submodules as independent git repositories.

Step 1: In a new path, add a `test_file.R` to the `submodule_one` git repo.

	emacs test_file.R
	...
	## make some changes and save.

	git add test_file.R

	git commit -m "Demonstrate updating of submodules"

	git push

Step 2: Go to the `main_repository`, to pull and add changes made in
the submodule to the main_repository.

Go to the main repository,

	cd main_repository

You now need to update the submodules, with the following command.

	git submodule update

Then, when you run `pull` it will gather the new changes present in
all the submodules present in the `.gitmodules` file.

	git pull ##

Check the status, to notice that the changes in the submodule haven't
been added to the main_repository

	git status

Add the submodule,

	git add submodule_one

Commit the changes to the submodule

	git commit -m "Update submodule"

Push the changes of the sumodule to the main_repository. Note, that
the actual files still are on a a different git repository. This is
only useful for people who are cloning the main_repository with all
the submodules.

	git push


## Clone the main respository with all submodules

To clone the main_repository with all the submodules, [git --version >
2.13]. This example shows a main_repository with 2 submodules.



	git clone --recurse-submodules -j 2 git@github.com:nturaga/main_repository


	--recurse-submodules[=<pathspec]
		   After the clone is created, initialize and clone submodules within based on the provided
		   pathspec. If no pathspec is provided, all submodules are initialized and cloned.
		   Submodules are initialized and cloned using their default settings. The resulting clone
		   has submodule.active set to the provided pathspec, or "." (meaning all submodules) if no
		   pathspec is provided. This is equivalent to running git submodule update --init
		   --recursive immediately after the clone is finished. This option is ignored if the
		   cloned repository does not have a worktree/checkout (i.e. if any of --no-checkout/-n,
		   --bare, or --mirror is given)


	-j <n>, --jobs <n>
		   The number of submodules fetched at the same time. Defaults to the submodule.fetchJobs option.
