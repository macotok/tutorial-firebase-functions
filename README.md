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

## fucntions

- functions を呼び出す

```
const addRequest = firebase.functions().httpsCallable('addRequest');
```

## firestore rules

- 読み許可

```
rules_version = '2';
service cloud.firestore {
  match /databases/{database}/documents {
    match /{document=**} {
    	allow read;
      allow write: if false;
    }
  }
}
```

## firestore

- collection の data 取得

```
const ref = firebase.firestore().collection('requests');

ref.onSnapshot((snapshot) => {
  let requests = [];
  snapshot.forEach((doc) => {
    requests.push({ ...doc.data(), id: doc.id });
  });
```

## firestore data trigger

- firestore に data が格納されたかを検知
- collection、id を取得できる

```
functions.firestore.document('/{collection}/{id}').onCreate((snap, context) => {
    console.log(snap.data());
    const collection = context.params.collection;
    const id = context.params.id;
});
```
