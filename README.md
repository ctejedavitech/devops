Certainly! Here's the content converted into a GitHub README format:

---

# LDAPS Query Tool Enhancements

This document explains the improvements made to the LDAPS query tool for secure LDAP querying. These enhancements ensure secure connections, modern Python practices, and compatibility updates.

## Features

- **Secure LDAPS Connection**: Connect securely to LDAPS servers using SSL/TLS.
- **Improved File Management**: Use Python's context managers for file operations.
- **Python 3 Compatibility**: Adjusted syntax for Python 3 compatibility.

## Detailed Changes

### Imported LDAPS related options:
- **LDAP Module Import**: 
  ```python
  import ldap
  ```
  (this was already present in the original code).

- **CA Certificate Path**:
  ```python
  ldap.set_option(ldap.OPT_X_TLS_CACERTFILE, '/path/to/your/cacert.pem')
  ```
  Specifies the location of the CA certificate that the client will use to validate the server's certificate.

### Server Connection Initialization:
- **LDAPS Protocol**:
  ```python
  self._server = "ldaps://172.26.38.110"
  ```
  Updated the protocol to `ldaps`, the standard for LDAP over SSL.

### Connection Settings:
- **Server Initialization**:
  ```python
  l = ldap.initialize(self._server)
  ```
  Preferred method over the deprecated `ldap.open()`. It initializes a connection to the LDAP server.

- **Handle Referrals**:
  ```python
  l.set_option(ldap.OPT_REFERRALS, 0)
  ```
  This option handles Microsoft Active Directory servers, ensuring the client doesn't chase referrals. It might be optional depending on your LDAP setup.

- **LDAP Version**:
  ```python
  l.set_option(ldap.OPT_PROTOCOL_VERSION, 3)
  ```
  Specifies the use of LDAP v3. LDAP v2 is outdated.

- **Server Certificate Validation**:
  ```python
  l.set_option(ldap.OPT_X_TLS_REQUIRE_CERT, ldap.OPT_X_TLS_DEMAND)
  ```
  This enforces that the server's certificate must be valid and trusted.

- **Start TLS**:
  ```python
  l.start_tls_s()
  ```
  Initiates a StartTLS extended operation. Might not be necessary in some `ldaps://` setups.

### Binding:
- **Synchronous Binding**:
  ```python
  l.simple_bind_s(self._bindDN, self._bindPW)
  ```
  The `_s` ensures synchronous operation.

### File Management:
- **Context Manager for File Handling**:
  ```python
  with open(new_authz_file, "w") as new_authz_stream:
  ```
  Ensures proper closure of file handles.

### Comments & Print Statements:
- **Python 3 Print Syntax**:
  ```python
  print("updates to groups, recreating authz")
  ```

---

This README is organized for clarity and better understanding. Adjustments can be made based on the repository's specifics and requirements.
