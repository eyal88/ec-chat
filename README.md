# ec-chat
Vue chat component

## Install
```
npm i --save ec-chat
```

## Usage

### Import the component
```
import ECChat from "ec-chat";
```

### Register the component
```
components: {
  "ec-chat": ECChat
}
```

### Import style sheet
```
@import "~ec-chat/dist/ECChat.css";
```

### Use it
```
<ec-chat
  :messages="messages"
  :fetching-messages="fetchingMessages"
  :user="user._id"
  :send-message="sendMessage"
  :get-user-by-id="getUserById"
/>
```

| Name | Type | Description |
|---|---|---|
| messages | [Message] | Array of all messages, sorted by creation date |
| fetching-messages | Boolean | Is fetching messages |
| user | String | Logged user id |
| send-message | Function(message: Message) => Promise | Function for sending a new message |
| get-user-by-id | Function(userId: String) => User | Function for getting user object by user id |

### Objects

#### Message
```
{
  user: String, // user id
  created: Date,
  text: String
}
```

#### User
```
{
  _id: String,
  name: String,
  color: String // Hex
}
```

## Project setup
```
npm install
```

### Compiles and hot-reloads for development
```
npm run serve
```

### Compiles and minifies for production
```
npm run build
```

### Lints and fixes files
```
npm run lint
```

### Customize configuration
See [Configuration Reference](https://cli.vuejs.org/config/).
