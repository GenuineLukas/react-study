# Spam Detector

Naive Bayes classifier

→ the combination of Bayes Theorem and the naive assumption that the two variables are independent when they may not be.

say there is 25 spam and 75 no spam emails.

![Untitled](Spam%20Detector%20caa030674ded4d0a8691a1b2668a1143/Untitled.png)

if an e-mail contains the word “buy”, what is the probability that it is spam?

→ 20/25 = 4/5 = 80%

![Untitled](Spam%20Detector%20caa030674ded4d0a8691a1b2668a1143/Untitled%201.png)

If an e-mail contains the word “cheap”, what is the probability that it is spam?

→ 15/25 = 3/5 = 60%

![Untitled](Spam%20Detector%20caa030674ded4d0a8691a1b2668a1143/Untitled%202.png)

If an e-mail contains the words “buy” and “cheap”, what is the probability that it is spam?

100% ⇒ feels very skeptical

Let’s make a naive assumption

given we’ve found 5 “Buy” and 10 “Cheap” out of 100 e-mails, we make a naive assumption that 0.5% of the emails contain both “Buy” and “Cheap”.

make the similar assumption to our case too.

![Untitled](Spam%20Detector%20caa030674ded4d0a8691a1b2668a1143/Untitled%203.png)

![Untitled](Spam%20Detector%20caa030674ded4d0a8691a1b2668a1143/Untitled%204.png)

![Untitled](Spam%20Detector%20caa030674ded4d0a8691a1b2668a1143/Untitled%205.png)

Now the same quiz.

If as e-mail contains the words “buy” and “cheap”, what is the probability that it is spam?

$$
\frac{12}{12+\frac{2}{3}}=\frac{36}{38} = 94.737\%
$$

![Untitled](Spam%20Detector%20caa030674ded4d0a8691a1b2668a1143/Untitled%206.png)