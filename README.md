# wireshark-http-traffic-analysis
Demonstrating Cleartext Credential Exposure (CWE-319) using Wireshark and Python local server.
# Traffic Analysis Lab: Υποκλοπή Στοιχείων σε Μη Κρυπτογραφημένο Δίκτυο (HTTP)

## Περιγραφή του Project
Σε αυτό το εργαστήριο έστησα έναν τοπικό web server και ανέλυσα την κίνηση του δικτύου με το εργαλείο **Wireshark**. Στόχος ήταν να δω στην πράξη γιατί το απλό πρωτόκολλο **HTTP** είναι ανασφαλές και πώς ένας τρίτος μπορεί να υποκλέψει κωδικούς πρόσβασης αν δεν υπάρχει κρυπτογράφηση (HTTPS).

---

## Εργαλεία που Χρησιμοποιήθηκαν
* **Wireshark:** Πρόγραμμα καταγραφής και ανάλυσης πακέτων δικτύου (packet sniffing).
* **Python:** Ενσωματωμένος web server (`python -m http.server 8080`).
* **HTML:** Μια απλή τοπική φόρμα εισόδου (`index.html`) με πεδία Username και Password.
* **Loopback Interface (`127.0.0.1`):** Η εσωτερική κάρτα δικτύου του υπολογιστή για την παρακολούθηση της τοπικής κίνησης.

---

## Βήματα που Ακολούθησα

### 1. Στήσιμο Περιβάλλοντος και Αποστολή Δεδομένων
1. Έφτιαξα μια απλή φόρμα εισόδου σε HTML.
2. Ξεκίνησα έναν τοπικό server μέσω Python στη θύρα 8080.
3. Άνοιξα το Wireshark στην κάρτα **Loopback Adapter** και ξεκίνησα την καταγραφή.
4. Συμπλήρωσα τα στοιχεία:
   * **Username:** `admin`
   * **Password:** `SuperSecretPassword123`
5. Πάτησα υποβολή και σταμάτησα την καταγραφή.

---

## Ευρήματα και Ανάλυση

### Βήμα Α: Εντοπισμός του Πακέτου Εισόδου
Χρησιμοποίησα το display filter του Wireshark:
```wireshark
http.request.method == "POST"
