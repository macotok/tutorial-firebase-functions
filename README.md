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

## Auth Triggers

- user create
- firestore の users collection に create

```
exports.newUserSignup = functions.auth.user().onCreate((user) => {
  return admin.firestore().collection('users').doc(user.uid).set({
    email: user.email,
    upvotedOn: [],
  });
});
```

- user delete
- firestore の users collection で delete

```
exports.userDeleted = functions.auth.user().onDelete((user) => {
  const doc = admin.firestore().collection('users').doc(user.uid);
  return doc.delete();
});
```

## Adding Requests

- functions を呼び出す

```
const addRequest = firebase.functions().httpsCallable('addRequest');
```
