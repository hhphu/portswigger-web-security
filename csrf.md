# Cross-site Request Forgery

## CSRF vulnerability with no defenses

## Test Cases for Lab #5 - CSRF where Token is Tied to Non-Session Cookie
**URL:** https://portswigger.net/web-security/csrf/bypassing-token-validation/lab-token-tied-to-non-session-cookie
<details>
  <summary> Test Case 1: Check if CSRF Token is Tied to User Session  </summary>

  | **Steps** | **Expected Result** |
  |-----------|--------------------|
  | Log in as `wiener:peter` and capture the CSRF token. | There should be `csrfKey` in the Cookie-session and `csrf` in the request body  |
  | Modify the `csrf` token so it becomes invalid | The application should reject the token as it is invalid. Otherwise, we can conclude the `csrf` and the `csrfKey` are not tied |
  | 1. Log in as `carlos:montoya` and capture the user CSRF token. <br > 2. Log in as `wiener:peter` and replace wiener's csrf token with carlos'| The application should reject the token as it does not belong to wiener. <br> We can conclude `csrf` and `csrfKey` go together|


</details>

<details>
  <summary> Test Case 2: Submit Valid CSRF Token and Cookie from Another User  </summary>

  | **Steps** | **Expected Result** |
  |-----------|--------------------|
  | Log in as `wiener:peter` and capture CSRF token and csrfKey cookie. | |
  | Log in as `carlos:montoya` in another session. | |
  | Use `wiener:peter`’s CSRF token and csrfKey cookie in `carlos:montoya`’s request. | The request should be rejected if tokens are session-bound. |

</details>

<details>
  <summary> Test Case 3: Inject CSRF Key Cookie via HTTP Header Injection  </summary>

  | **Steps** | **Expected Result** |
  |-----------|--------------------|
  | Inject a csrfKey cookie into the victim’s session via HTTP header injection. | |
  | Capture the email change request. | |
  | Submit the request with the injected csrfKey cookie. | The attack should succeed if the vulnerability exists. |

</details>

<details>
  <summary> Test Case 4: Execute a CSRF Attack with a Known CSRF Token  </summary>

  | **Steps** | **Expected Result** |
  |-----------|--------------------|
  | Construct a malicious CSRF attack containing a valid CSRF token. | |
  | Trick the victim into executing the request (e.g., via phishing link). | |
  | Observe if the victim’s email is changed without their consent. | If the vulnerability exists, the email change should succeed. |

</details>

### **Summary:**
These test cases evaluate whether CSRF protection is implemented correctly and identify weaknesses in CSRF token handling and session security.

