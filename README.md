# Revisiting the Conflict-Resolving Problem from a Semantic Perspective

In this repository we provide the code and data for the paper ``Revisiting the Conflict-Resolving Problem from a Semantic Perspective''. The contents of two folders are introduced in the following. 

+ `Scripts` contains the scripts to execute our approach.
+ `Data` contains the information of the projects/commits we use, and also contains the results.

## 1 Preparation

In this work, the scripts contain both `python` and `shell` scripts, and the benchmark we use is  `java` projects. Therefore, we need the environments to execute all three languages. Furthermore, we leverage the tool `evosuite` and LLM `GPT-4`.

- `shell`: Linux installs the shell interpreter by default, e.g., Bash. On windows, you can install Git Bash or WSL to execute the shell script.
- `python`: We provide the file `requirements.txt`, which includes all the libraries in our python environment and you can execute ` python -m pip install -r requirements.txt` to install these libraries.
- `java`: We install several different versions of JDK to increase the success rate of compilation, including the Oracle JDK 8/11/17. You need to install them and export to the environment variables `ORACELJAVA/8/11/17`. We need to update the `PATH` to switch to difference java versions during compilation. We use `maven` to compile and execute tests, and the version is 3.9.6.
- `evsouite`: The version of `evosuite` is 1.0.6, and you can download it from the [website](https://www.evosuite.org/downloads/).
- `gpt-4`: We use the API `GPT-4 Turbo`.

## 2 Scripts

In this section, we introduce the scripts of our approach, which are located in the folder `Scripts`.


- `build_clone.sh` clones the projects we use in our work from github, and it will record the clone results, i.e., clone success or clone fail.
- `build_compile.sh` compiles the projects, and it will record the compile results. We leverage `GNU Parallel` to compile the projects in parallel, and the number of parallel compilation is set to 10.
- `build_conflicts.sh` leverages `git merge` to merge the two commits and reproduce the conflicts.
- `build_create_version.sh` creates two intermediate versions of the commit A and commit B. It replaces the conflicting parts with the code of A and B respectively.
- `build_test.sh` executes the existing tests of the projects.
- `build_evosuite.sh` leverages `evosuite` to generate the test cases for each conflicting case.
- `execute_evosuite_test.py` runs the tests generated by `evosuite`.
- `run_gpt.py` leverages the API of GPT-4 to generate tests and also execute the generated tests.

You can execute `runtotal.sh` to finish the whole process.

## 3 Data
In the folder `Data`, we provide the projects and commit we use. In addition, we provide the execution results of all the previous stages. Furthermore, the prompt of our GPT-based test generation can be found in `run_gpt.py`.