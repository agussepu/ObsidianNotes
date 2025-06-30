Gracias por compartir tu reporte, está **muy bien escrito para ser tu primero**, y solo necesita algunos ajustes para adaptarse 100% al modelo profesional de HackerOne.

Acá te dejo tu reporte **modificado, mejorado y listo para enviar**, en el formato exacto que HackerOne espera:

---

# ✅ Title

Account Takeover via direct reuse of `mzpStickySession` / `MZPSID` cookies and leaked JWT

---

# ✅ Description

## Summary:

An attacker can perform **Account Takeover (ATO)** by reusing the session cookies `mzpStickySession` and `MZPSID` from another user. When these cookies are injected into an authenticated session (user A), the server responds with a valid **JWT token for user B**, effectively leaking their identity and authorization.

This leaked JWT can then be used to access and modify personal data (such as first and last name) of the victim (user B), all from the attacker’s session (user A), without knowing user B’s credentials or requiring any interaction.

---

## Steps To Reproduce:
1. Log in as **user A** in one browser/session, and as **user B** in another. In this case I used firefox
    
2. From user B’s session, extract the cookies `mzpStickySession` and `MZPSID`.
    
3. Replace user A’s cookies with user B’s values for `mzpStickySession` and `MZPSID`
    
4. Navigate to `/account/overview` as user A with the modified cookies.
    
5. Observe that the server now returns a **JWT for user B** in the `Authorization: Bearer <token>` response header.
    
6. With this token and the reused cookies, send a `PUT` request to update user B’s personal information.

### Sample request (using leaked JWT and cookies):

```http
PUT /customer-data/api/v2/basicData HTTP/1.1
Host: www.zooplus.com
Authorization: Bearer <JWT_OBTENIDO_DEL_USUARIO_B>
Content-Type: application/json
Cookie: mzpStickySession="b525f0a78e9777fc"; MZPSID=F5A811D36DD4F8EFEF91BC7A894D6FA1;
Origin: https://www.zooplus.com
Referer: https://www.zooplus.com/account/customer/editPersonalInformation

{"firstName":"Hack","lastName":"Hacked"}
```

7. Log in again as user B and observe the modified personal data.
    

---

## Supporting Material / References:

- Screenshot 1: Parallel sessions of user A and B
    
- Screenshot 2: Cookie replacement
    
- Screenshot 3: JWT received in response
    
- Screenshot 4: Profile data of user B modified by attacker session
    

---

# ✅ Impact

- **Partial Account Takeover (ATO)**: attacker can modify personal information of another user without consent.
    
- **JWT leakage** via cookie manipulation, violating session boundaries.
    
- **Exploitable without user interaction** or password knowledge.
    
- Risk of **identity theft, reputational damage, or escalation to full account control** depending on what the JWT allows.
    

This issue demonstrates a **critical weakness in session isolation and authorization enforcement**. It is reproducible, automatable, and affects the integrity of user accounts.

---

### ✅ Severity Suggestion: `Critical`

---

¿Querés que también te prepare el texto para la caja de “Severity Justification” o lo armás vos? Si querés, te lo dejo listo también.