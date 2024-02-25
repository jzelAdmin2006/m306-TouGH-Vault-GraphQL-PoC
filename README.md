# m306-TouGH-Vault-GraphQL-PoC

**Important**: Replace the placeholders with <> with your own data.

- Request for first 100 repos

```bash
curl --request POST \
 --url https://api.github.com/graphql \
 --header 'Authorization: Bearer <YOUR_GITHUB_PERSONAL_ACCESS_TOKEN>' \
 --header 'Content-Type: application/json' \
 --header 'User-Agent: insomnia/8.6.1' \
 --data '{"query":"query getContributions($login: String!, $contributionTypes: [RepositoryContributionType]) {\n user(login: $login) {\n repositoriesContributedTo(contributionTypes: $contributionTypes, first: 100, includeUserRepositories: true, orderBy: {field: STARGAZERS, direction: DESC}) {\n pageInfo {\n hasNextPage\n endCursor\n }\n nodes {\n nameWithOwner\n }\n }\n }\n}\n","operationName":"getContributions","variables":"{\n \"login\": \"<YOUR_GITHUB_ACCOUNT_NAME>\",\n \"contributionTypes\": [\n \"COMMIT\",\n \"REPOSITORY\"\n ]\n}"}'
```

- Request for each next 100 repos
  
  ```bash
  curl --request POST \
    --url https://api.github.com/graphql \
    --header 'Authorization: Bearer <YOUR_GITHUB_PERSONAL_ACCESS_TOKEN>' \
    --header 'Content-Type: application/json' \
    --header 'User-Agent: insomnia/8.6.1' \
    --data '{"query":"query getContributions($login: String!, $contributionTypes: [RepositoryContributionType], $afterCursor: String) {\n  user(login: $login) {\n    repositoriesContributedTo(contributionTypes: $contributionTypes, first: 100, after: $afterCursor, includeUserRepositories: true, orderBy: {field: STARGAZERS, direction: DESC}) {\n      pageInfo {\n        hasNextPage\n        endCursor\n      }\n      nodes {\n        nameWithOwner\n      }\n    }\n  }\n}\n","operationName":"getContributions","variables":"{\n\t\"login\": \"<YOUR_GITHUB_ACCOUNT_NAME>\",\n\t\"contributionTypes\": [\n\t\t\"COMMIT\",\n\t\t\"REPOSITORY\"\n\t],\n\t\"afterCursor\": \"<AFTER_CURSOR_RETURNED_FROM_REQUEST_BEFORE>\"\n}"}'
  ```