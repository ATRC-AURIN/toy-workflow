# ATRC-AURIN Toy Workflow

This 'toy' workflow is an exercise to illustrate the way tools can be composed into workflows. It consists of a number of toy tools that perform basic operations on arrays of numbers, and a Workflow Runner that can take a workflow definition file and run the toy tools in a given order, providing it with initial values and passing results through the sequential workflow operations. 

Note: there's no code in this repository – this Readme is just an guide directing you to the other repositories. 

### The example workflow:

![toy workflow diagram](https://user-images.githubusercontent.com/28953011/152715452-1be015dc-90b3-4d82-b8a5-4f092f74e0a9.png)

### The toy tools:

#### Fibonnaci Sequence generator:
https://github.com/AURIN-OFFICE/atrc-fibonacci-tool   
Test script: `./fibonacci.sh`

#### List AdderSubtractor:
https://github.com/AURIN-OFFICE/atrc-adder-subtracter   
Test script: `./adder_test_script.sh`

#### List MultiplierDivider:
https://github.com/AURIN-OFFICE/atrc-multiplier-divider   
Test script: `./multiplier_test_script.sh`

#### List Transform:
https://github.com/AURIN-OFFICE/atrc-list-transform   
Test script: `./list_head_test_script.sh`

### The Workflow Runner:

https://github.com/AURIN-OFFICE/atrc-workflow-runner

### Want to run it yourself?

- Make sure you have Docker installed and running locally
- Make sure you have [Node](https://nodejs.org/en/download/) installed
- Clone the workflow runner code to your local machine
- Run the [toy_setup_script.sh](https://github.com/AURIN-OFFICE/atrc-workflow-runner/blob/main/toy_setup_script.sh)
- Run `npm run workflow`
- You should see outputs for each operation in the workflow written to a timestamped directory in `./tmp/`

### What functionality is included / not included?

The Workflow Runner takes as it's starting point `workflow.yaml` workflow definition files. These files can contain actual values of input parameters in the file, or reference to input files that can also be provided - as they are in the `/initial_data/` directory in the workflow runner. It then assumes that the docker images of the tools referenced in the workflow definition are present, and runs each operation, passing parameters as required. If an expected output is not produced by a tool, the runner will throw an error. 

Obviously, hand-writing a `workflow.yaml` file for each different workflow a user might want to run is not a practical way to work. So, eventually alongside the 'Workflow Runner'-like component of the platform, there'll be a 'Workflow Composer'. This will read the definition of each tool's parameters in their `tool_schema.yaml` and `operation_schema.yaml` files, and allow users to produce a `workflow.yaml` that knows how to meet its parameters which can then be passed to the Workflow Runner. Keeping these concerns separate under the hood will likely be useful going forward. 
