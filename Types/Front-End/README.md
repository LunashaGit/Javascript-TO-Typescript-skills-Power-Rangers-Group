# Welcome in the NEW CHAPTER Front End Types !

## Links

- [Back-End](./../Back-End/)
- [Full-Stack](./../Full-Stack/)
- [Root](https://github.com/LunashaGit/Javascript-TO-Typescript-skills-Power-Rangers-Group)

## Front-End

### Types Props

```tsx
type AppProps = {
  message: string;
  /** "I'm a Message" */
  count: number;
  /** 36 */
  disabled: boolean;
  /** array of a type! -> true or false */
  names: string[];
  /** string literals to specify exact string values, with a union type to join them together ["test1", "test2"]*/
  status: "waiting" | "success";
  /** an object with known properties (but could have more at runtime) */
  obj: {
    id: number;
    title: string;
  };
  /** array of objects! (common)
   *
   * obj = {
   * id: 1,
   * title: "i'm a title"}
   */
  objArr: {
    id: string;
    title: string;
  }[];
  /** any non-primitive value - can't access any properties (NOT COMMON but useful as placeholder)
   * objArr = [{id: 1, title: "i'm a title1"}, {id: 2, title: "i'm a title2"}]
   */
  obj2: object;
  /** an interface with no required properties - (NOT COMMON, except for things like `React.Component<{}, State>`)
   * obj2 = {id: 1, title: "i'm a title"}
   */
  obj3: {};
  /** a dict object with any number of properties of the same type */
  dict1: {
    [key: string]: MyTypeHere;
  };
  dict2: Record<string, MyTypeHere>; // equivalent to dict1
  /** function that doesn't take or return anything (VERY COMMON) */
  onClick: () => void;
  /** function with named prop (VERY COMMON) */
  onChange: (id: number) => void;
  /** function type syntax that takes an event (VERY COMMON) */
  onChange: (event: React.ChangeEvent<HTMLInputElement>) => void;
  /** alternative function type syntax that takes an event (VERY COMMON) */
  onClick(event: React.MouseEvent<HTMLButtonElement>): void;
  /** any function as long as you don't invoke it (not recommended) */
  onSomething: Function;
  /** an optional prop (VERY COMMON!) */
  optional?: OptionalType;
  /** when passing down the state setter function returned by `useState` to a child component. `number` is an example, swap out with whatever the type of your state */
  setState: React.Dispatch<React.SetStateAction<number>>;
};
```

### Props Types in Function

```tsx
type TypeChildren = {
  children: React.ReactNode;
};

type TypePlayer = {
  id: number;
  name: string;
  email: string;
  password: string;
  trees: Object[];
  createdAt: string;
  updatedAt: string;
};

export const AuthProvider = ({ children }: TypeChildren) => {
  // provides the authentication to the different components
  const [auth, setAuth] = useLocalStorage("user", null);
  const [players, setPlayers] = useState<string>();
  const [player, setPlayer] = useState<TypePlayer>({} as TypePlayer);

  const [trees, setTrees] = useState<Object[]>([]);
  const [singleTree, setSingleTree] = useState<Array<String>>([]);
  const [userTrees, setUserTrees] = useState<Object[]>([]);

  useEffect(() => {
    let isMounted = true; // mounted true = the component is loaded to the site
    const controller = new AbortController();

    const getPlayer = async () => {
      try {
        const { data } = await axios.get(PLAYER_URL + auth);
        isMounted && setPlayer(response);
      } catch (err) {
        console.log(err);
      }
    };
    getPlayer();

    const getTreesByOwner = async () => {
      try {
        const response = await axios.get(USER_TREES_URL + auth);
        //console.log(response.data)
        isMounted && setUserTrees(response.data[0].trees);
      } catch (err) {
        console.log(err);
      }
    };
    getTreesByOwner();

    return () => {
      // we clean up function of the useEffect
      isMounted = false; // means we don't mount the component and
      controller.abort();
    };
  }, []);

  return (
    <AuthContext.Provider
      value={{
        auth,
        setAuth,
        players,
        setPlayers,
        player,
        setPlayer,
        userTrees,
        setUserTrees,
        singleTree,
        setSingleTree,
      }}
    >
      {children}
    </AuthContext.Provider>
  );
};
```

### Explaination of the code above:

#### Props Types

```tsx
type TypeChildren = {
  children: React.ReactNode;
};
```

I created a Type for my Children Props, to say what type of children I want to pass to my component (Name). In this case, I want to pass a ReactNode (a ReactNode is a ReactChild, which is a ReactElement or a ReactText, which is a string or a number).

And how i used it in my component:

```tsx
export const AuthProvider = ({ children }: TypeChildren) => { ... }
```

But i can also use other type of props, if the props is different like a string, a number, a boolean, an object, an array, a function, etc.

```tsx
function MyComponent({ name, age }: { name: string; age: number }) {
  return (
    <div>
      Hello, {props.name}, {props.age} Years-old,
    </div>
  );
}
```

#### UseState Types

```tsx
const [players, setPlayers] = useState<string>();
const [player, setPlayer] = useState<TypePlayer>({} as TypePlayer);
```

After the useState, you need to specify the type of the variable you want to use. In this case, I want to use a string and an object. I created a Type for my object, and I used it in my useState.

You can see here that I used the Type i created before "TypePLayer", and I used it in my useState. So now, I can use the TypePlayer in my component.

It's better to do {} as TypePlayer, because if you don't do that, you will have an error, because you can't use an object without initializing it. Or you can use the useState like this:

```tsx
const [player, setPlayer] = useState<TypePlayer>({
  id: null,
  name: null,
  email: null,
  password: null,
  trees: [],
  createdAt: null,
  updatedAt: null,
});
```

But it's better to use {} as TypePlayer, because it's more readable. And you can use the useState like this:

And sometimes, you don't need every information of your object, so you can use Partial<TypePlayer> instead of TypePlayer.

```tsx
TypePlayer = {
  id?: number;
  name?: string;
  email: string;
  password: string;
  trees: Object[];
  createdAt: string;
  updatedAt: string;
};
// or
const [player, setPlayer] = useState<Partial<TypePlayer>>({} as TypePlayer);
```

Give a "?:" to the properties you don't need. And you can use Partial<TypePlayer> instead of TypePlayer. Partial<TypePlayer> means that all the properties of TypePlayer are optional. But for me, it's better to use ?:, after this you know exactly what you need and what you don't need.

You can give some default values, like this:

```tsx
type Roles = "admin" | "user" | "guest";

type User = {
  name: string;
  age: number;
  role: Roles;
};
```

Then you know, you can't have another role than admin, user or guest.

We can do some conditional types, like this:

```tsx
type User = {
  name: string;
  age: number;
  role: Roles;
};

type UserWithId = User & { id: number };

type UserWithIdAndEmail = User & { id: number; email: string };

type UserWithIdAndEmailAndPhone = User & {
  id: number;
  email: string;
  phone: string;
};

type UserWithIdAndEmailAndPhoneAndAddress = User & {
  id: number;
  email: string;
  phone: string;
  address: string;
};
```

We will take the type of the User to complete the type of the UserWithId, UserWithIdAndEmail, etc.

And integrate to my function

```tsx
const [user, setUser] = useState<UserWithIdAndEmailAndPhoneAndAddress>(
  {} as UserWithIdAndEmailAndPhoneAndAddress
);
```

For Debugging, i use Any, but it's not a good practice, because you can have some errors, and you don't know where it comes from.

```tsx
const [user, setUser] = useState<any>(null);
```

The "any" give the possibility to use any type of variable. (String) "Fred": any means that the variable "fred" can be a string, a number, a boolean, an object, an array, a function, etc.
