# tutorial-firebase-functions

localhost 起動

```
$ firebase serve
```

firebase functions のみデプロイ

```
$ firebase deploy --only functions
```

## authentication

- emial と password で認証するときに使用する関数

sign up

```
firebase.auth().createUserWithEmailAndPassword(email, password)
```

sign in

```
firebase.auth().signInWithEmailAndPassword(email, password)
```

sign out

```
firebase.auth().signOut()
```

login してるかどうかの判定

```
firebase.auth().onAuthStateChanged((user) => {
  if (user) {

  }
  .
  .
  .
});
```

## functions

user create

```
exports.newUserSignup = functions.auth.user().onCreate((user) => {
  console.log('user created', user.email, user.uid);
});
```

user delete

```
exports.userDeleted = functions.auth.user().onDelete((user) => {
  console.log('user deleted', user.email, user.uid);
});
```
