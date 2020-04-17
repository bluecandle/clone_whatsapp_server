# Chapter 5
Testing with Jest in server code.

## modification in package.json
te-test 설치 이후, 

we will need to specify the file pattern that we would like to transform with ts-jest, by adding the following section to package.json:

    {
    "jest": {
        "transform": {
        "^.+\\.(js|jsx|ts|tsx)$": "<rootDir>/node_modules/ts-jest"
        }
    }

    // 이건 이번 튜토리얼에 한정되어 필요한 설정.
    "jest-junit": {
    "outputDirectory": "./test-results"
    },

    ## 얘네는 넣는건가 아닌건가?? 일단 튜토리얼 상태에서, 넣으면 오류남.
    "globals": {
            "ts-jest": {
                "diagnostics": false
            }
        },
        "globalSetup": "<rootDir>/tests/global-setup.ts",
        "reporters": [
            "default",
            "jest-junit"
        ]
    },
    
### package : apollo-server-testing

    yarn add --dev apollo-server-testing

Now we're gonna test the chatsquery in our GraphQL schema. To do so, we will setup an Apollo Client and send a query request to our back-end, and then we will match the received response with a pre-defined snapshot. Luckily, we don't have to set an actual client, since the tests and the implementation of the back-end live right next to each other, thus, we will install a package which will help us achieving so

### snapshot
The .toMatchSnapshot() matcher will call the toString() method on the examined object and will test it against a predefined snapshot. The snapshot will automatically be created once we run the test for the first time and will be stored under the __snapshot__directory.
This means that the first test run will always pass. This is useful because you can later on observe and adjust manually the snapshot manually without having to write it from scratch.

<b>bAlways be sure to observe the snapshot before moving on! The received result isn't necessarily what you'd expect. </b> Also it's not a good practice to store production data in the snapshot because it's subject to changes. Normally we would set up another instance of the DB for testing purposes, but since our DB is a mock and doesn't represent real data, there's no need to at this stage.