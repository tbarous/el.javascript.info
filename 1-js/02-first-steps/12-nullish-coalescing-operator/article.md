# Μηδενικός τελεστής συγχώνευσης '??'

[recent browser="new"]

Ο μηδενικός τελεστής συγχώνευσης `??` παρέχει μια σύντομη σύνταξη για την επιλογή μιας πρώτης `καθορισμένης` μεταβλητής από τη λίστα.

Το αποτέλεσμα της `a ?? b` είναι:
- `a` εάν δεν είναι `null` ή `undefined`,
- `b`, αλλίως.

Ετσι είναι `x = a ?? b` ισοδύναμο με:

```js
result = (a !== null && a !== undefined) ? a : b;
```


Εδώ είναι ένα μεγαλύτερο παράδειγμα.

Φανταστείτε, έχουμε έναν χρήστη και υπάρχουν μεταβλητές `firstName`, `lastName` ή `nickName` για το όνομα, το επώνυμο και το ψευδώνυμό τους. Όλα αυτά μπορεί να είναι ακαθόριστα, εάν ο χρήστης αποφασίσει να μην εισαγάγει καμία τιμή.

Θα θέλαμε να εμφανίσουμε το όνομα χρήστη: μία από αυτές τις τρεις μεταβλητές ή να δείξουμε "Anonymous" εάν δεν έχει οριστεί τίποτα.

Ας χρησιμοποιήσουμε τον τελεστή `??` για να επιλέξουμε τον πρώτο καθορισμένο:

```js run
let user;

alert(user ?? "Anonymous"); // Anonymous
```

Of course, if `user` had any value except `null/undefined`, then we would see it instead:

```js run
let user = "John";

alert(user ?? "Anonymous"); // John
```

We can also use a sequence of `??` to select the first value from a list that isn't `null/undefined`.

Let's say we have a user's data in variables `firstName`, `lastName` or `nickName`. All of them may be undefined, if the user decided not to enter a value.

We'd like to display the user name using one of these variables, or show "Anonymous" if all of them are undefined.

Let's use the `??` operator for that:
>>>>>>> 181cc781ab6c55fe8c43887a0c060db7f93fb0ca

```js run
let firstName = null;
let lastName = null;
let nickName = "Supercoder";

<<<<<<< HEAD
// εμφάνιση της πρώτης μη μηδενικής / μη καθορισμένης τιμής
=======
// shows the first defined value:
>>>>>>> 181cc781ab6c55fe8c43887a0c060db7f93fb0ca
*!*
alert(firstName ?? lastName ?? nickName ?? "Anonymous"); // Supercoder
*/!*
```

## Σύγκριση με ||

Ο τελεστής OR `||` μπορεί να χρησιμοποιηθεί με τον ίδιο τρόπο όπως `??`. Στην πραγματικότητα, μπορούμε να αντικαταστήσουμε το `??` με το `||` στον παραπάνω κώδικα και να πάρουμε το ίδιο αποτέλεσμα, όπως περιγράφηκε στο [προηγούμενο κεφάλαιο](info:logical-operators#or-finds-the-first-truthy-value)


Οι σημαντικές διαφορές είναι:
- `||` επιστρέφει την πρώτη *truthy* τιμή.
- `??` επιστρέφει την πρώτη *defined* τιμή.
Αυτό έχει μεγάλη σημασία όταν θα θέλαμε να αντιμετωπίσουμε το `null/undefined` διαφορετικά από το `0`.

Για παράδειγμα, δείτε αυτό:

```js run
let firstName = null;
let lastName = null;
let nickName = "Supercoder";
>>>>>>> 181cc781ab6c55fe8c43887a0c060db7f93fb0ca

// shows the first truthy value:
*!*
alert(firstName || lastName || nickName || "Anonymous"); // Supercoder
*/!*
```

Αυτό ορίζει το `height` σε `100` εάν δεν έχει οριστεί.

Ας συκγρίνουμε το `||`:

```js run
let height = 0;

alert(height || 100); // 100
alert(height ?? 100); // 0
```

Εδώ, `height || 100` αντιμετωπίζει το μηδέν ύψος ως μη ορισμένο, όπως το `null`, το `undefined` ή οποιαδήποτε άλλη τιμή falsy.
Έτσι το αποτέλεσμα είναι `100`.

Το `height ?? 100` επιστρέφει το `100` μόνο εάν το `height` είναι `null` ή `undefined`. Έτσι, το `alert` δείχνει την τιμή ύψους `0` "ως έχει".

Ποια συμπεριφορά είναι καλύτερη εξαρτάται από μια συγκεκριμένη περίπτωση χρήσης. Όταν το μηδέν ύψος είναι μια έγκυρη τιμή, τότε το `??` είναι προτιμότερο.

## Προτεραιότητα

Η προτεραιότητα του τελεστή `??` είναι μάλλον χαμηλή: `5` στο
[πίνακα MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Operator_Precedence#Table).

Για αυτό το `??` αξιολογείται μετά τις υπόλοιπες λειτουργίες, αλλά πριν από το `=` και το `?`.

Εάν χρεαστούμε να επιλέξουμε μια τιμή με `??` σε μια σύνθετη έκφραση, τότε να λαμβάνεται υπ όψιν να προσθέσετε παρενθέσεις:

```js run
let height = null;
let width = null;

// Προσοχή: χρησιμοποιηστε παρενθέσεις
let area = (height ?? 100) * (width ?? 50);

alert(area); // 5000
```
Διαφορετικά, εάν παραλείψουμε παρενθέσεις, το `*` έχει την υψηλότερη προτεραιότητα από το `??` και θα τρέξει πρώτα.


Αυτό θα λειτουργούσε ακριβώς το ίδιο με:

```js
// μάλλον δεν είναι σωστό
let area = height ?? (100 * width) ?? 50;
```

Υπάρχει επίσης ένας σχετικός περιορισμός σε επίπεδο γλώσσας.

**Για λόγους ασφαλείας, απαγορεύεται η χρήση του τελεστή `??` με `&&` και `||`.**


```js
// without parentheses
let area = height ?? 100 * width ?? 50;

// ...works the same as this (probably not what we want):
let area = height ?? (100 * width) ?? 50;
```

Ο παρακάτω κώδικας ενεργοποιεί ένα σφάλμα σύνταξης:

```js run
let x = 1 && 2 ?? 3; // Syntax error
```
Ο περιορισμός είναι σίγουρα συζητήσιμος, αλλά προστέθηκε στις προδιαγραφές γλώσσας με σκοπό να αποφευχθούν λάθη προγραμματισμού, καθώς οι άνθρωποι αρχίζουν να αλλάζουν σε `??` από `||`.

Χρησιμοποιήστε ρητές παρενθέσεις για να το επιλύσετε:

```js run
*!*
let x = (1 && 2) ?? 3; // Λειτουργεί
*/!*

alert(x); // 2
```

## Περίληψη


- Ο μηδενικός τελεστής συγχώνευσης `??` παρέχει έναν σύντομο τρόπο για να επιλέξετε μια "defined" τιμή από τη λίστα.


    Χρησιμοποιείται για την ανάθεση προεπιλεγμένων τιμών σε μεταβλητές:

    ```js
    // set height=100, εαν height είναι null ή undefined
    height = height ?? 100;
    ```

- Ο τελεστής `??` έχει πολύ χαμηλή προτεραιότητα, λίγο υψηλότερος από το `?` και το `=`.
- Απαγορεύεται η χρήση του με `||`" ή `&&` χωρίς ρητές παρενθέσεις.
