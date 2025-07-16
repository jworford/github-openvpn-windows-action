# Security Policy

## Supported Versions

| Version | Supported          |
| ------- | ------------------ |
| 1.x     | :white_check_mark: |

## Reporting a Vulnerability

If you discover a security vulnerability in this GitHub Action, please report it by:

1. **DO NOT** create a public GitHub issue for security vulnerabilities
2. Email the maintainer directly with details about the vulnerability
3. Include steps to reproduce the issue
4. Provide any relevant logs or screenshots (with sensitive information redacted)

## Security Considerations

When using this action, please keep in mind:

- **Never commit OpenVPN configuration files, usernames, or passwords to your repository**
- Always use GitHub Secrets for sensitive information
- Regularly rotate your OpenVPN credentials
- Use the minimum required permissions for your OpenVPN user account
- Monitor your action logs for any suspicious activity

## Best Practices

1. Store all sensitive data in GitHub Secrets
2. Use short-lived credentials when possible
3. Regularly audit your OpenVPN server access logs
4. Keep your OpenVPN server software updated
5. Use strong, unique passwords for OpenVPN accounts
6. The action automatically cleans up processes and temporary files
7. Monitor your workflows to ensure cleanup steps complete successfully

## Updates

Security updates will be released as patch versions. Please keep your action reference updated to the latest version.
