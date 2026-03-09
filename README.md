# WhatsApp Matrix Bridge

A Matrix-WhatsApp puppeting bridge that enables communication between Matrix and WhatsApp platforms.

## Features

- Bridge Matrix rooms to WhatsApp conversations
- Message synchronization between platforms
- User puppeting support
- Asynchronous event handling
- Docker support for easy deployment

## Project Structure

```
whatsapp/
├── src/                      # Source code
│   ├── __init__.py
│   ├── main.py              # Entry point
│   ├── bridge.py            # Main bridge logic
│   ├── config.py            # Configuration management
│   ├── matrix_client.py     # Matrix protocol handler
│   └── whatsapp_client.py   # WhatsApp protocol handler
├── tests/                    # Test suite
│   ├── conftest.py
│   ├── test_bridge.py
│   ├── test_matrix_client.py
│   └── test_whatsapp_client.py
├── docs/                     # Documentation
├── config/                   # Configuration files
├── scripts/                  # Utility scripts
├── requirements.txt          # Python dependencies
├── setup.py                  # Package setup
├── Dockerfile                # Docker image definition
├── docker-compose.yml        # Docker compose configuration
├── .env.example              # Environment variables template
└── README.md                 # This file
```

## Installation

### Prerequisites

- Python 3.8+
- pip or conda
- Docker (optional)

### Local Setup

1. Clone the repository:
```bash
git clone https://github.com/Xtf302-hub/whatsapp.git
cd whatsapp
```

2. Create a virtual environment:
```bash
python -m venv venv
source venv/bin/activate  # On Windows: venv\Scripts\activate
```

3. Install dependencies:
```bash
pip install -r requirements.txt
```

4. Configure environment:
```bash
cp .env.example .env
# Edit .env with your Matrix and WhatsApp credentials
```

5. Run the bridge:
```bash
python -m src.main
```

### Docker Setup

1. Copy the environment template:
```bash
cp .env.example .env
# Edit .env with your credentials
```

2. Build and run with Docker Compose:
```bash
docker-compose up -d
```

## Configuration

The bridge requires the following environment variables:

- `MATRIX_URL`: Matrix homeserver URL (e.g., http://localhost:8008)
- `MATRIX_TOKEN`: Matrix authentication token
- `MATRIX_USER_ID`: Matrix user ID (e.g., @bot:example.com)
- `WHATSAPP_PHONE`: WhatsApp phone number with country code (e.g., +1234567890)
- `LOG_LEVEL`: Logging level (default: INFO)
- `DATABASE_URL`: Database connection URL (optional)

See `.env.example` for a template.

## Development

### Running Tests

```bash
pytest tests/ -v
pytest tests/ --cov=src  # With coverage
```

### Code Quality

```bash
black src/  # Format code
flake8 src/  # Lint code
mypy src/   # Type checking
```

## API Documentation

### Bridge Class

The main `Bridge` class manages communication between Matrix and WhatsApp:

```python
from src.bridge import Bridge
from src.config import load_config

config = load_config()
bridge = Bridge(config)
await bridge.start()
```

### Matrix Client

Handles Matrix protocol communication:

```python
from src.matrix_client import MatrixClient

client = MatrixClient("http://localhost:8008", "token")
await client.connect()
await client.send_message("!room:example.com", "Hello")
```

### WhatsApp Client

Handles WhatsApp protocol communication:

```python
from src.whatsapp_client import WhatsAppClient

client = WhatsAppClient("+1234567890")
await client.connect()
await client.send_message("contact@example.com", "Hello")
```

## Contributing

Contributions are welcome! Please:

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/amazing-feature`)
3. Commit your changes (`git commit -m 'Add amazing feature'`)
4. Push to the branch (`git push origin feature/amazing-feature`)
5. Open a Pull Request

## License

MIT License - see LICENSE file for details

## Support

For issues and questions, please create an issue on the GitHub repository.

## Roadmap

- [ ] Full Matrix protocol implementation
- [ ] Full WhatsApp protocol integration
- [ ] Message formatting support
- [ ] File/media transfer
- [ ] Group chat support
- [ ] User profile synchronization
- [ ] End-to-end encryption support
