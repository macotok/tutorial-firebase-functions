# tutorial-firebase-functions

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
