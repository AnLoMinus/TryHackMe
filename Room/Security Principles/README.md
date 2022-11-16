![image](https://user-images.githubusercontent.com/51442719/202032560-11b7f5ed-fe5f-464f-8f20-206cc9e09418.png)

# [Security Principles](https://tryhackme.com/room/securityprinciples)
#### Learn about the security triad and common security models and principles.

---

- [Task 1  Introduction](#task-1--introduction)
- [Task 2  CIA](#task-2--cia)
- [Task 3  DAD](#task-3--dad)
- [Task 4  Fundamental Concepts of Security Models](#task-4--fundamental-concepts-of-security-models)
- [Task 5  Defence-in-Depth](#task-5--defence-in-depth)
- [Task 6  ISO/IEC 19249](#task-6--isoiec-19249)
- [Task 7  Zero Trust versus Trust but Verify](#task-7--zero-trust-versus-trust-but-verify)
- [Task 8  Threat versus Risk](#task-8--threat-versus-risk)
- [Task 9  Conclusion](#task-9--conclusion)

---

## Task 1  Introduction

![image](https://user-images.githubusercontent.com/51442719/202032585-d54f2f0e-3717-4161-a385-5c311e4b2f1d.png)

Security has become a buzzword; every company wants to claim its product or service is secure. But is it?

Before we start discussing the different security principles, it is vital to know the adversary against whom we are protecting our assets. Are you trying to stop a toddler from accessing your laptop? Or are you trying to protect a laptop that contains technical designs worth millions of dollars? Using the exact protection mechanisms against toddlers and industrial espionage actors would be ludicrous. Consequently, knowing our adversary is a must so we can learn about their attacks and start implementing appropriate security controls.

![image](https://user-images.githubusercontent.com/51442719/202032678-73b25599-47a4-4a98-b291-64757e3d083b.png)

It is impossible to achieve perfect security; no solution is 100% secure.  
Therefore, we try to improve our security posture to make it more difficult for our adversaries to gain access.

The objective of this room is to:

- Explain the security functions: Confidentiality, Integrity and Availability (CIA).
- Present the opposite of the security triad, CIA: Disclosure, Alteration, and Destruction/Denial (DAD).
- Introduce the fundamental concepts of security models, such as the Bell-LaPadula model.
- Explain security principles such as Defence-in-Depth, Zero Trust, and Trust but Verify.
- Introduce ISO/IEC 19249.
- Explain the difference between Vulnerability, Threat, and Risk.

---

## Task 2  CIA

![image](https://user-images.githubusercontent.com/51442719/202045216-0f9c871b-4913-4c20-8e9c-6484cf87b38e.png)


Before we can describe something as secure, we need to consider better what makes up security. When you want to judge the security of a system, you need to think in terms of the security triad: confidentiality, integrity, and availability (CIA).

- `Confidentiality` ensures that only the intended persons or recipients can access the data.
- `Integrity` aims to ensure that the data cannot be altered; moreover, we can detect any alteration if it occurs.
- `Availability` aims to ensure that the system or service is available when needed.

> # Let’s consider the CIA security triad in the case of placing an order for online shopping:

- `Confidentiality`: 
  - During online shopping, you expect your credit card number to be disclosed only to the entity that processes the payment. If you doubt that your credit card information will be disclosed to an untrusted party, you will most likely refrain from continuing with the transaction. Moreover, if a data breach results in the disclosure of personally identifiable information, including credit cards, the company will incur huge losses on multiple levels.
- `Integrity`: 
  - After filling out your order, if an intruder can alter the shipping address you have submitted, the package will be sent to someone else. Without data integrity, you might be very reluctant to place your order with this seller.
- `Availability`: 
  - To place your online order, you will either browse the store’s website or use its official app. If the service is unavailable, you won’t be able to browse the products or place an order. If you continue to face such technical issues, you might eventually give up and start looking for a different online store.


> # Let’s consider the CIA as it relates to patient records and related systems:

- `Confidentiality`: 
  - According to various laws in modern countries, healthcare providers must ensure and maintain the confidentiality of medical records. Consequently, healthcare providers can be held legally accountable if they illegally disclose their patients’ medical records.
- `Integrity`:
  - If a patient record is accidentally or maliciously altered, it can lead to the wrong treatment being administered, which, in turn, can lead to a life-threatening situation. Hence, the system would be useless and potentially harmful without ensuring the integrity of medical records.
- `Availability`: 
  - When a patient visits a clinic to follow up on their medical condition, the system must be available. An unavailable system would mean that the medical practitioner cannot access the patient’s records and consequently won’t know if any current symptoms are related to the patient’s medical history. This situation can make the medical diagnosis more challenging and error-prone.

The emphasis does not need to be the same on all three security functions. One example would be a university announcement; although it is usually not confidential, the document’s integrity is critical.

## Beyond CIA

Going one more step beyond the CIA security triad, we can think of:

- `Authenticity`: 
  - Authentic means not fraudulent or counterfeit. Authenticity is about ensuring that the document/file/data is from the claimed source.
- `Nonrepudiation`: 
  - Repudiate means refusing to recognize the validity of something. Nonrepudiation ensures that the original source cannot deny that they are the source of a particular document/file/data. This characteristic is indispensable for various domains, such as shopping, patient diagnosis, and banking.

These two requirements are closely related. The need to tell authentic files or orders from fake ones is indispensable. Moreover, ensuring that the other party cannot deny being the source is vital for many systems to be usable.

In online shopping, depending on your business, you might tolerate attempting to deliver a t-shirt with cash-on-delivery and learn later that the recipient never placed such an order. However, no company can tolerate shipping 1000 cars to discover that the order is fake. In the example of a shopping order, you want to confirm that the said customer indeed placed this order; that’s authenticity. Moreover, you want to ensure they cannot deny placing this order; that’s nonrepudiation.

As a company, if you receive a shipment order of 1000 cars, you need to ensure the authenticity of this order; moreover, the source should not be able to deny placing such an order. Without authenticity and nonrepudiation, the business cannot be conducted.

### Parkerian Hexad
In 1998, Donn Parker proposed the Parkerian Hexad, a set of six security elements. They are:

- Availability
- Utility
- Integrity
- Authenticity
- Confidentiality
- Possession

We have already covered four of the above six elements. Let's discuss the remaining two elements:

- `Utility`: 
  - Utility focuses on the usefulness of the information. For instance, a user might have lost the decryption key to access a laptop with encrypted storage. Although the user still has the laptop with its disk(s) intact, they cannot access them. In other words, although still available, the information is in a form that is not useful, i.e., of no utility.
- `Possession`: 
  - This security element requires that we protect the information from unauthorized taking, copying, or controlling. For instance, an adversary might take a backup drive, meaning we lose possession of the information as long as they have the drive. Alternatively, the adversary might succeed in encrypting our data using ransomware; this also leads to the loss of possession of the data.


---

## Task 3  DAD

---

## Task 4  Fundamental Concepts of Security Models

---

## Task 5  Defence-in-Depth

---

## Task 6  ISO/IEC 19249

---

## Task 7  Zero Trust versus Trust but Verify

---

## Task 8  Threat versus Risk

---

## Task 9  Conclusion
