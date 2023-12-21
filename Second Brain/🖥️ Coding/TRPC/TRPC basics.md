## Updating state 

Something I learned is that to update the state of  TRPC happens with the onSuccess hook. Example: 

```ts
  const getByDate = trpc.useQuery(["post.getByDate", { date: date }], {
    onSuccess: (data) => {
      setNotesList(data);
    },
  });
```

or with Mutation

```ts
  const insertMutation = trpc.useMutation(["post.insertOne"], {
    onSuccess: (newNote) => {
      router.push(`/note/${newNote.id}`);
    },
  });
```


## Why use TRPC vs REST? 

## TRPC Server side 

