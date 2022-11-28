# Week 9 Lab Report
## `grade.sh` Code Block
```
rm -rf student-submission/
git clone $1 student-submission
if [[ -f ./student-submission/ListExamples.java ]]; then
    echo "ListExamples was found in the repository."
else
    echo "ListExamples was not found in the repository."
    exit
fi 
cp TestListExamples.java ./student-submission
cp -r ./lib ./student-submission/lib
cd student-submission
set +e
# javac -cp .:lib/hamcrest-core-1.3.jar:lib/junit-4.13.2.jar *.java
# java -cp .:lib/hamcrest-core-1.3.jar:lib/junit-4.13.2.jar org.junit.runner.JUnitCore TestListExamples > compile-err.txt
javac -cp ".;lib/hamcrest-core-1.3.jar;lib/junit-4.13.2.jar" *.java
java -cp ".;lib/hamcrest-core-1.3.jar;lib/junit-4.13.2.jar" org.junit.runner.JUnitCore TestListExamples > compile-err.txt
grep -B 1 "Error:" compile-err.txt > tests-success.txt
testMerge=$( grep -c "testMerge" tests-success.txt )
testFilter=$( grep -c "testFilter" tests-success.txt )
testTotal=$(($testMerge + $testFilter))
if [[ $testTotal -eq 0 ]]; then
    echo "Passed all tests! Score: 2/2"
    exit
fi
if [[ $testMerge -eq 1 ]]; then
    echo "Failed testMerge."
fi
if [[ $testFilter -eq 1 ]]; then
    echo "Failed testFilter."
fi
if [[ $testTotal -eq 1 ]]; then
    echo "Score: 1/2"
    exit
fi
if [[ $testTotal -eq 2 ]]; then
    echo "Score: 0/2"
    exit
fi
```

## Screenshots of 3 Different Student Submissions

**Repo Link:** https://github.com/ucsd-cse15l-f22/list-methods-corrected
![](images\rp5-corrected.png)
**Repo Link:** https://github.com/ucsd-cse15l-f22/list-methods-lb3
![](images\rp5-lab3.png)
**Repo Link:** https://github.com/ucsd-cse15l-f22/list-methods-filename
![](images\rp5-filename.png)

## Tracing `grade.sh` for `list-methods-filename`

` rm -rf student-submission/ `

**Standard output:** Removes all of the files & directories in `student-submission` as well as the directory itself. After this command is performed, the home directory of `student-submission` will no longer contain a directory called `student-submission`.

**Standard error:** N/A

**Return code:** 0, since it succeeds.

`git clone $1 student-submission`

**Standard output:** This will clone the repository entered as the first argument into a new directory called `student-submission`. It will alter the contents of the home directory by adding a new directory with new contents.

**Standard error:** N/A

**Return code:** 0, since it succeeds.

`if [[ -f ./student-submission/ListExamples.java ]]; then`

**Condition Value:** False

**Reasoning:** The command inside the `if` statement checks if the correct file exists. If it does, it will return an exit code of 0 and an exit code of 1 if it fails. Since the correct file does not exist, it returns an exit code of 1 and fails the `if` statement condition.

`     echo "ListExamples was found in the repository."` 

**Does Not Run**

**Reasoning:** The `if` statement that this command belongs in failed.

`else`

**Condition Value:** True

**Reasoning:** Since the `if` statement failed (`if` statement condition resulted in an exit code of 1), this `else` statement is fulfilled.

`echo "ListExamples was not found in the repository."`

**Standard output:** The command prints out the following string into the terminal.

**Standard error:** N/A

**Return code:** 0

`exit`

**Standard output:** The program exits early. The rest of the lines after `exit` will no longer run.

**Standard error:** N/A

**Return code:** 0

As stated above, the rest of the script does not run since it ends up exiting early.



