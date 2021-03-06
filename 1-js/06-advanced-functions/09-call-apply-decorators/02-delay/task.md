importance: 5

---

# Διακοσμητής καθυστέρησης

Δημιούργησε ένα διακοσμητή `delay(f, ms)` που καθυστερεί κάθε κλήση της `f` χρόνο ίσο με `ms` δέκατα του δευτερολέπτου.

Για παράδειγμα:

```js
function f(x) {
  alert(x);
}

// δημιουργία συναρτήσεων-καλύμματα
let f1000 = delay(f, 1000);
let f1500 = delay(f, 1500);

f1000("τέστ"); // δείχνει τέστ μετά από 1000 δέκατα του δευτερολέπτου
f1500("τέστ"); // δείχνει τέστ μετά από 1500 δέκατα του δευτερολέπτου
```

Με άλλα λόγια, η `delay(f, ms)` επιστρέφει μια "καθυστερημένη κατά `ms`" εκδοχή της `f`.

Στον παραπάνω κώδικα, η `f` είναι μια συνάρτηση ενός μονού ορίσματος, αλλά η λύση σου πρέπει να περνάει όλα τα ορίσματα και το context `this`.
