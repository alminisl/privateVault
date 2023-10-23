**## Partial**

```type Worker = {  
  name: string;  
  profession: string;  
}// Not defining 'profession' is allowed  
const worker: Partial<Worker> = {  
  name: 'Jeroen'   
}
```

**## Required**

```
type Worker = {  
  name?: string;  
  profession?: string;  
}// You should defining 'name' and 'profession'  
const worker: Required<Worker> = {  
  name: 'Jeroen',  
  profession: 'Developer',  
}
```

**## Readonly**


```
type Worker = {  
  name: string;  
  profession: string;  
}const worker: Readonly<Worker> = {  
  name: 'Jeroen',  
  profession: 'Developer',  
}worker.name = 'Bob'; // Not allowed
```

**## Pick**

```
type Worker = {  
  name: string;  
  profession: string;  
  isWorking: boolean;  
}// Only 'name' and 'isWorking' are included  
const worker: Pick<Worker, 'name' | 'isWorking'> = {  
  name: 'Jeroen',  
  isWorking: true,  
}
```

**## Omit**

```
type Worker = {  
  name: string;  
  profession: string;  
  isWorking: boolean;  
}// 'profession' is now excluded  
const worker: Omit<Worker, 'profession'> = {  
  name: 'Jeroen',  
  isWorking: true,  
}
```

**## Record**

```
type Worker = 'developer' | 'architect'  
type Person = { name: string }// a worker object has now 'developer' or 'architect' as keys  
const worker: Record<Worker, Person> = {  
  'developer': { name: 'Jeroen' },  
  'architect': { name: 'Bob' },  
}
```


**## NonNullable**

```
// Returns only 'Jeroen'  
const worker: NonNullable<'Jeroen', undefined, null>;
```

**## Extract**

```
type Worker = {  
  name: string;  
  age: string;  
  isWorking: boolean  
}type Person = {  
  name: string;  
  age: string;  
}// 'name' or 'age' is both in type Person and Worker therefore only allowed   
const worker: Extract<keyof Worker, keyof Person> = 'name' || 'age';
```

**## Exclude**

```
type Worker = {  
  name: string;  
  age: string;  
  isWorking: boolean  
}type Person = {  
  name: string;  
  age: string;  
}// 'isWorking' is not in type Person and therefor only allowed   
const worker: Exclude<keyof Worker, keyof Person> = 'isWorking';
```