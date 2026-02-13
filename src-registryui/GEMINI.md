# Component: Docker Registry UI front by NGINX

## Purpose

This Nginx instance acts as a TLS termination proxy for the private Docker Registry running on port 5000.

## Configuration Rules

### 1. SSL/TLS

- **Protocols**: We are currently supporting `TLSv1` through `TLSv1.2` for compatibility, but we aim to deprecate `TLSv1` and `TLSv1.1` in favor of `TLSv1.3` soon.
- **Certs**: Certificates are mapped to `/etc/nginx/certs/`.

### 2. Docker Registry Specifics

- **Upload Limits**: The registry requires large file uploads for image layers.
  - `client_max_body_size` MUST be set to `0` (unlimited).
- **Headers**: Ensure `Docker-Distribution-Api-Version` is passed if required.
- **Compatibility**: We maintain a block for legacy Docker clients (pre-1.6) that send bad user agents.

### 3. Future Improvements

- Enable HTTP/2.
- Harden security headers (HSTS, X-Frame-Options).
