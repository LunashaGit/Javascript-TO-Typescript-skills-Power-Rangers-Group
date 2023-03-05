# Welcome in the NEW CHAPTER Back End Types !

## Links

- [Front-End](./../Front-End/)
- [Full-Stack](./../Full-Stack/)
- [Root](https://github.com/LunashaGit/Javascript-TO-Typescript-skills-Power-Rangers-Group)

## FOR BOTH PARTS

You can types, interfaces outside of your files, and create your type FILE
type.ts

```
export Interface User = {
  username: string;
  email: string;
  password: string;
  color: string;
}

export type User = {
  username: string;
  email: string;
  password: string;
  color: string;
}
```

The EXPORT can be used to import in your files and be more readable,

React :

```tsx
import { User } from "./types";

function App({ User }: User){...}
```

Express :

```ts
import { User } from "./interface";

const userSchema: Schema<IUser> = new Schema({...})
```

## Back-End

You use Express & Mongoose,

### Types Interfaces

```ts
Request: This type represents the incoming HTTP request object in ExpressJS. It includes properties such as params, query, and body, which allow for accessing the different parts of the request.

Response: This type represents the outgoing HTTP response object in ExpressJS. It includes methods such as send, json, and status, which allow for sending data back to the client.

NextFunction: This type represents the next middleware function in the ExpressJS middleware chain. It is used to pass control to the next middleware function in the stack.

Model<T extends Document>: This type represents a Mongoose model. It is used to create, read, update, and delete documents from a MongoDB database.

Document: This type represents a Mongoose document. It includes all the properties and methods defined in the schema for the document.

Schema: This type represents a Mongoose schema. It is used to define the structure and behavior of a document in a MongoDB collection.

SchemaDefinition: This type represents the definition of a Mongoose schema. It is used to specify the properties and their types for a document in a MongoDB collection.

Query<T extends Document, DocType extends T | null = T>: This type represents a Mongoose query. It is used to find, update, and delete documents from a MongoDB database.

Aggregate: This type represents a Mongoose aggregate. It is used to perform aggregation operations on a MongoDB collection.
```

### Types Models

```ts
import { Schema, Document, Model } from "mongoose";

interface IUser extends Document {
  username: string;
  email: string;
  password: string;
  color: string;
}

interface IUserModel extends Model<IUser> {
  signup: (
    username: string,
    email: string,
    password: string,
    color: string
  ) => Promise<IUser>;
}

const userSchema: Schema<IUser> = new Schema({
  username: {
    type: String,
    required: true,
    unique: true,
    minLength: 4,
    maxLength: 30,
  },
  email: {
    type: String,
    required: true,
    unique: true,
    maxLength: 255,
  },
  password: {
    type: String,
    required: true,
  },
  color: {
    type: String,
    required: true,
    minLength: 4,
    maxLength: 7,
  },
});

// --------- Sign up
userSchema.statics.signup = async function (username, email, password, color) {
  // Check every fields requirements
  if (!email || !username || !password || !color) {
    throw Error("All fields need to be filled");
  }
  if (!validator.isAlphanumeric(username) && !validator.isAlpha(username)) {
    throw Error("The username must contain only letters and numbers");
  }
  if (color.charAt(0) != "#" || !validator.isHexColor(color)) {
    throw Error(
      `The color entered is not hexadecimal color, be sure you put '#' in front of the combination`
    );
  }
  if (!validator.isEmail(email)) {
    throw Error("The email address entered is not valid");
  }
  if (!validator.isStrongPassword(password)) {
    throw Error(
      "The password must contain 8 character minimum, with an uppercase, a number and a symbol"
    );
  }

  // Check existence in DB
  const emailExist = await this.findOne({ email });
  const usernameExist = await this.findOne({ username });
  if (emailExist) {
    throw Error("Email already used, please enter another adress");
  }
  if (usernameExist) {
    throw Error("Username already used, please enter another name");
  }
  // Protecting and hashing the password
  const salt = await bcrypt.genSalt(10);
  const hash = await bcrypt.hash(password, salt);
  // Create the user in DB as you sign up
  const user = await this.create({ username, email, password: hash, color });
  // Create the playerin DB as you sign up
  const player = await Player.create({
    username,
    email,
    password: hash,
    color,
  });
  // Attribute three tree as you signed in
  const attributeTree = await Tree.getThree(username);
  // Attribute the player leaf in his wallet as he signed up
  addLeafs(username);

  return user, player;
};
```

The interface IUser extends Document and defines the properties of a user, including username, email, password, and color.

The interface IUserModel extends Model< IUser > and defines a static method signup that takes in username, email, password, and color, and returns a Promise of IUser.

The userSchema variable creates a new Mongoose schema for a user, with properties such as username, email, password, and color.

### Types Controllers

```ts
import { Request, Response } from "express";
import Player from "../models/Player";

const getAccount = async (req: Request, res: Response) => {
  const { username } = req.params;
  const player = await Player.findOne({ username: username }).select(
    "-password"
  );

  try {
    if (!player) {
      throw Error(`This username doesn't exist`);
    }

    res.status(200).json(player);
    return player;
  } catch (error) {
    res.status(400).json({ error: error.message });
  }
};
```

The Request interface defines the expected properties and methods of an incoming HTTP request, such as the request method, URL, headers, and body. The Response interface defines the expected properties and methods of an outgoing HTTP response, such as the response status code, headers, and body.

### Types Middlewares

```ts
import { Request, Response, NextFunction } from "express";
import jwt from "jsonwebtoken";
import Player from "../models/Player";

const auth = async (req: Request, res: Response, next: NextFunction) => {
  try {
    const token = req.header("Authorization")?.replace("Bearer ", "");
    const decoded = jwt.verify(token, process.env.JWT_SECRET);
    const player = await Player.findOne({
      _id: decoded._id,
      "tokens.token": token,
    });

    if (!player) {
      throw new Error();
    }

    req.token = token;
    req.player = player;
    next();
  } catch (error) {
    res.status(401).send({ error: "Please authenticate." });
  }
};
```

The NextFunction interface is a callback function that is used to pass control to the next middleware function in the request-response cycle.

### Types Routes

```ts
import { Router } from "express";
import { getAccount } from "../controllers/account";
import auth from "../middlewares/auth";

const router = Router();

router.get("/account/:username", auth, getAccount);

export default router;
```
