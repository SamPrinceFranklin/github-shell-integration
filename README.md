# GitHub API Data Retrieval Script

This script allows users to communicate with the GitHub API and retrieve information. It is written in Bash and provides a convenient way to interact with the GitHub API using a GitHub token and a REST API endpoint.

## Usage

To use this script, please follow the instructions below:

1. Ensure that you have a valid GitHub token. If you don't have one, you can generate it from your GitHub account settings.
2. Provide the GitHub token and the REST API endpoint as input when executing the script.

```bash
bashCopy code$ ./script.sh [your GitHub token] [REST expression]
```

## Script Details

* **Author:** Sam Prince Franklin K
* **Version:** v1

## Dependencies

This script requires the following dependencies:

* `curl`: Command-line tool for making HTTP requests.

## Functionality

1. **Argument Validation**: The script checks if the required arguments (GitHub token and REST expression) are provided. If not, it displays the correct usage and exits.
2. **Variable Assignment**: The provided arguments (GitHub token and REST expression) are assigned to the respective variables (`GITHUB_TOKEN` and `GITHUB_API_REST`).
3. **GitHub API Header**: The script sets the GitHub API header for specifying the response format (`GITHUB_API_HEADER_ACCEPT`). It uses the `Accept` header with the value `application/vnd.github.v3+json`.
4. **Temporary File Creation**: A temporary file is created to store the API response. The file is created using the `mktemp` command, and its path is assigned to the `TMPFILE` variable.
5. **REST API Call Function**: The script defines a function named `rest_call` that makes a REST API call to GitHub and stores the response in the temporary file. It uses the `curl` command with the provided API URL, the GitHub API header, and the provided GitHub token.
6. **Pagination Check**: The script checks if the API response uses pagination by examining the `Link` header in the response. It retrieves the last page number from the `Link` header using the `curl` command, `grep`, and `sed`.
7. **API Call**: If the API response is not paginated (single page), the script makes a single REST API call using the provided REST API endpoint. The `rest_call` function is invoked with the API URL constructed from the provided endpoint.
8. **Pagination Handling**: If the API response is paginated, the script makes multiple REST API calls to retrieve data from all pages. It uses a `for` loop to iterate from page 1 to the last page number obtained earlier. The `rest_call` function is invoked for each page, appending the `page` parameter to the API URL.
9. **API Response Display**: Finally, the script displays the contents of the temporary file (API response) using the `cat` command.

## Usage in DevOps

This script can be utilized in DevOps workflows for various purposes, including but not limited to:

* Retrieving information about GitHub repositories, branches, commits, issues, pull requests, etc.
* Automating tasks related to managing GitHub repositories, such as creating or updating issues, adding or modifying labels, and more.
* Integrating with other tools or scripts to perform actions based on the retrieved GitHub API data.
* Building custom GitHub monitoring or reporting systems by collecting and processing data from the API.
* Incorporating GitHub data into CI/CD pipelines for making informed decisions or triggering actions based on specific conditions.

By leveraging this script, DevOps teams can efficiently interact with the GitHub API and integrate GitHub-related functionalities into their automation and deployment processes.

## License

This script is licensed under the [MIT License](https://chat.openai.com/LICENSE).
