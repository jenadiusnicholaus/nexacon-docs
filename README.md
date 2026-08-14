# Nexacon Documentation

Official documentation for Nexacon SDKs.

## Overview

This repository contains comprehensive documentation for the Nexacon SDKs.

- **Flutter SDK** - Cross-platform audio/video calling for Android, iOS, Linux, macOS, and Windows

Additional SDKs for other platforms will be added here once tested and stable.

## Related SDKs

- **Nexacon Messaging SDK** - Real-time chat messaging with presence, typing indicators, and message history. Docs at [nexacon-messaging.readthedocs.io](https://nexacon-messaging.readthedocs.io/)

## Documentation

The official documentation is hosted at [https://docs.nexacon.africa](https://docs.nexacon.africa).

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
│   ├── flutter-sdk/         # Flutter SDK documentation (calls)
│   └── guides/             # Additional guides
```

## Features

The Nexacon Flutter SDK provides the following core features:

- **Authentication** - User login, token management, and session handling
- **Calls** - Audio and video calling with WebRTC
- **Devices** - Register devices for push notifications
- **Rooms** - Group call management
- **Presence** - User online status and last seen

## Contributing

To contribute to the documentation:

1. Fork this repository
2. Create a feature branch
3. Make your changes
4. Submit a pull request

## Support

- **Documentation**: https://docs.nexacon.africa
- **GitHub Issues**: https://github.com/jenadiusnicholaus/nexacon-docs/issues
- **Email**: support@nexacon.africa

## License

MIT License - see LICENSE file for details.
