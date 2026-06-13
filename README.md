# Nexacon Documentation

Official documentation for all Nexacon SDKs across multiple platforms and programming languages.

## Overview

This repository contains comprehensive documentation for the Nexacon API SDKs, including:

- **Flutter SDK** - Cross-platform mobile and desktop applications
- **JavaScript SDK** - Browser and Node.js applications
- **React Native SDK** - iOS and Android mobile applications
- **Python SDK** - Server-side and desktop applications
- **Java SDK** - Android and server-side applications
- **Go SDK** - Server-side and microservices
- **PHP SDK** - Web applications
- **Ruby SDK** - Web applications
- **C# SDK** - .NET applications

## Documentation

The official documentation is hosted at [https://docs.nexacon.com](https://docs.nexacon.com).

### Building Locally

To build the documentation locally:

```bash
# Install dependencies
pip install -r requirements.txt

# Build the documentation
cd docs
make html

# View the documentation
open _build/html/index.html
```

## Structure

```
nexacon-docs/
├── .readthedocs.yaml          # Read the Docs configuration
├── requirements.txt           # Python dependencies
├── docs/
│   ├── conf.py              # Sphinx configuration
│   ├── index.rst            # Main landing page
│   ├── getting-started.rst  # Quick start overview
│   ├── installation.rst     # Installation guide
│   ├── flutter-sdk/         # Flutter SDK documentation
│   ├── js-sdk/              # JavaScript SDK documentation
│   ├── react-native-sdk/    # React Native SDK documentation
│   ├── python-sdk/         # Python SDK documentation
│   ├── java-sdk/           # Java SDK documentation
│   ├── go-sdk/             # Go SDK documentation
│   ├── php-sdk/            # PHP SDK documentation
│   ├── ruby-sdk/           # Ruby SDK documentation
│   ├── csharp-sdk/         # C# SDK documentation
│   └── guides/             # Additional guides
```

## Features

All Nexacon SDKs provide the following core features:

- **Authentication** - User login, token management, and session handling
- **Messaging** - Send and receive messages with delivery receipts
- **Calls** - Audio and video calling with WebRTC
- **Devices** - Register devices for push notifications
- **Rooms** - Group chat management
- **Presence** - User online status and last seen

## Contributing

To contribute to the documentation:

1. Fork this repository
2. Create a feature branch
3. Make your changes
4. Submit a pull request

## Support

- **Documentation**: https://docs.nexacon.com
- **GitHub Issues**: https://github.com/nexacon/nexacon-docs/issues
- **Email**: support@nexacon.com

## License

MIT License - see LICENSE file for details.
