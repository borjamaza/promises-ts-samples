# Promises Simple Fetch Sample

In this sample we are continuing to understand the promises concept, using typescript.

We will start from sample [00 Simple Ajax] and we start using Fetch.

[00 Simple Ajax]: https://github.com/Lemoncode/promises-ts-samples/tree/master/00%20Simple%20Ajax "Lemoncode GitHub"


## Steps to build it

We will start from sample _00 simple ajax_:

- Install dependencies.
- Modify the sample: Chaining Promises
- Running the project.


## Building the project

We are going to install the dependencies. In this case, we have de same dependencies like the first sample, then we must run in command prompt:

```Batch
npm install
```

## Modify the sample: Chaining Promises

We can modify the promises using fetch. Now, the getListOfMembers method will have a promise with fetch:

```javascript
getListOfMembers() : Promise<Array<MemberEntity>> {
    return fetch('https://api.github.com/orgs/lemoncode/members')
      .then((response) => this.checkStatus(response))
      .then((response) => this.parseJSON(response)
      .then((response) => {return Promise.resolve(this.mapGitHubMembersToMemberEntityCollection(response))})
    );
}
```

One of the great features of promises is the ability to chain them together. In this sample, we can have the need to check the status and parse de JSon for each response. And you can chain specifics methods for each step: First, check status, then, parse the object, and then convert a JS Object.
At the end, you will answer with a promose.resolve.

If something is wrong, you will enter by catch code.

- Now we are going to cause an error. And we'll expect the error message in the webBrowser. First, we must add a catch code:

```javascript
getListOfMembers() : Promise<Array<MemberEntity>> {
  return fetch('https://api.github.com/orgs/lemoncode/members')
    .then((response) => this.checkStatus(response))
    .then((response) => this.parseJSON(response)
    .then((response) => {return Promise.resolve(this.mapGitHubMembersToMemberEntityCollection(response))})
    .catch((error) => this.throwError(error))
  );
}
```

And also, we are going to provoke the error if the name is Braulio, for example:

```javascript
// ... (in mapGitHubMembersToMemberEntityCollection method)
member.id = gitHubMember.id;
member.login = gitHubMember.login;
member.avatar_url = gitHubMember.avatar_url;

if (member.id=1457912){
  let error = new Error(`<p>${member.id} shouldn't be in the response...</p>`);
  throw error;
}
return member;
```

Now, In order to configure the response error, we have to add a new method:

```javascript
private throwError(error){
  document.write("<p>Ops! something wrong! We are so embarrased..</p>");
  console.log(error);
  return Promise.reject(error);
}
```

## Running the project

Now, we only need start de project

```bash
npm start
```
