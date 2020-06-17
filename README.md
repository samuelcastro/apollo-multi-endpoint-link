## Apollo link which add an api directive to fetch data from multi endpoints


### Install
```bash
   npm i @habx/apollo-multi-endpoint-link
```

### Setup
```typescript
  new ApolloClient({
    link: ApolloLink.from([
      new MultiAPILink({
          endpoints: {
              housings: 'https://housings.api',
              projects: 'https://projects.api',
              ...
          },
          createHttpLink: () => new HttpLink({ ... }),
        }),
    ])
  })
```

##### API
```typescript
  new MultiAPILink(config, request)
```

###### config

| Parameter      | Description                                                                                                 | Default        | Required |
|----------------|-------------------------------------------------------------------------------------------------------------|----------------|----------|
| endpoints      | Dictionary of endpoints                                                                                     |                | Yes      |
| createHttpLink | Function to generate http link like [apollo-link-http](https://www.apollographql.com/docs/link/links/http/) |                | Yes      |
| createWsLink   | Function to generate wsLink like [apollo-link-ws](https://www.apollographql.com/docs/link/links/ws/)        |                | No       |
| wsSuffix       | Suffix added to endpoint for subscriptions queries                                                          | /subscriptions | No       |
| httpSuffix     | Suffix added to endpoint for http queries                                                                   | /graphql       | No       |
### Queries
```graphql
  query projectList @api(name: projects) {
    projects {
      nodes {
        id
        name
      }
    }
  }
````
