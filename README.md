# Server Panel

A comprehensive server management panel similar to Pterodactyl, built with Node.js/Express backend and React frontend.

## Features

- **Dashboard**: Real-time overview of all servers with CPU, RAM, and storage metrics
- **Server Management**: Add, edit, and delete servers with SSH connectivity
- **File Manager**: Browse, upload, download, and edit server files via SFTP
- **Console**: Real-time server console with SSH command execution
- **User Management**: Admin controls for managing users and permissions
- **Authentication**: Secure JWT-based authentication
- **Real-time Monitoring**: Live server status and resource tracking
- **SSH Integration**: Full SSH/SFTP support for remote operations

## Project Structure

```
server-panel/
├── backend/                 # Express.js API
│   ├── src/
│   │   ├── controllers/    # Business logic
│   │   ├── models/         # MongoDB schemas
│   │   ├── routes/         # API endpoints
│   │   ├── middleware/     # Auth & utilities
│   │   ├── utils/          # Helper functions (SSH)
│   │   └── index.js        # Entry point
│   ├── package.json
│   ├── .env.example
│   └── Dockerfile
│
├── frontend/               # React app
│   ├── src/
│   │   ├── pages/         # Main pages
│   │   ├── components/    # Reusable components
│   │   ├── App.jsx
│   │   └── index.jsx
│   ├── public/
│   └── package.json
│
├── docs/                   # Documentation
│   ├── GETTING_STARTED.md
│   ├── API.md
│   ├── SSH_GUIDE.md
│   └── DEVELOPMENT.md
│
└── README.md
```

## Technology Stack

### Backend
- **Node.js & Express.js** - Server framework
- **MongoDB** - NoSQL database
- **JWT** - Authentication
- **SSH2** - SSH/SFTP for remote server operations
- **Bcrypt** - Password hashing

### Frontend
- **React 18** - UI framework
- **React Router** - Navigation
- **Axios** - HTTP client
- **Lucide React** - Icons

## Quick Start

### Prerequisites
- Node.js (v14+)
- MongoDB
- npm or yarn

### 1. Backend Setup

```bash
cd backend
npm install
cp .env.example .env
```

Edit `.env`:
```
MONGODB_URI=mongodb://localhost:27017/server-panel
JWT_SECRET=your-secret-key-here
PORT=5000
```

Start MongoDB:
```bash
mongod
```

Run backend:
```bash
npm run dev
```

### 2. Frontend Setup

```bash
cd frontend
npm install
npm start
```

### 3. Create Admin User

Use the installation script to create the admin account automatically:
- Windows: run `setup.bat` and enter the admin username, email, password, first name, and last name when prompted.
- macOS / Linux: run `setup.sh` and enter the same values.

If you need to create manually, use MongoDB and make sure the password is hashed or use the backend registration endpoint.

### 4. Start the Application

Run the start script:
- Windows: `start.bat`
- Linux/macOS: `./start.sh`

The application will be available at:
- **http://localhost:5000** (Frontend + API)

The backend automatically builds the frontend and serves it alongside the API.

- `GET /api/servers` - List all user servers
- `POST /api/servers` - Create new server
- `GET /api/servers/:id` - Get server details
- `PUT /api/servers/:id` - Update server
- `DELETE /api/servers/:id` - Delete server
- `GET /api/servers/:id/status` - Get server status (SSH)
- `POST /api/servers/test-connection` - Test SSH connection

### Files (SSH/SFTP)
- `GET /api/files/list` - List files in directory
- `GET /api/files/content` - Get file content
- `POST /api/files/upload` - Upload file
- `PUT /api/files` - Edit file
- `DELETE /api/files` - Delete file

### Console (SSH)
- `GET /api/console/logs` - Get console logs
- `POST /api/console/execute` - Execute remote command
- `DELETE /api/console/logs/:serverId` - Clear logs

### Dashboard
- `GET /api/dashboard/stats` - Get dashboard statistics
- `GET /api/dashboard/system` - Get system info

### Users
- `GET /api/users` - List all users (admin)
- `GET /api/users/:id` - Get user details
- `PUT /api/users/:id` - Update user
- `DELETE /api/users/:id` - Delete user (admin)

## SSH Features

The panel integrates with SSH/SFTP for:

- **Remote Command Execution**: Run any shell command on servers
- **File Management**: Browse, edit, upload, download files
- **System Monitoring**: Get CPU, RAM, disk usage in real-time
- **Server Status**: Check online/offline status
- **Connection Testing**: Verify SSH credentials before adding

See [SSH_GUIDE.md](docs/SSH_GUIDE.md) for detailed SSH usage.

## Configuration

### Backend Environment Variables

```
MONGODB_URI=mongodb://localhost:27017/server-panel
JWT_SECRET=your_strong_secret_key
PORT=5000
NODE_ENV=development
CORS_ORIGIN=http://localhost:3000
MAX_FILE_SIZE=104857600
```

### Frontend Environment Variables

```
REACT_APP_API_URL=http://localhost:5000
```

## Docker Setup

### Using Docker Compose

```bash
docker-compose up
```

This starts:
- MongoDB on port 27017
- Backend API on port 5000
- Frontend on port 3000

## Development

### Running in Dev Mode

**Backend:**
```bash
cd backend
npm run dev
```

**Frontend:**
```bash
cd frontend
npm start
```

### Building for Production

```bash
cd frontend
npm run build
```

## Security

### Best Practices

1. **SSH Security**
   - Use SSH keys instead of passwords
   - Restrict SSH access by IP
   - Disable root login
   - Change default SSH port

2. **API Security**
   - Use strong JWT secret
   - Enable HTTPS in production
   - Implement rate limiting
   - Validate all inputs

3. **Database Security**
   - Enable MongoDB authentication
   - Use strong database passwords
   - Regular backups
   - Encrypt sensitive data

4. **Server Security**
   - Keep dependencies updated
   - Use environment variables for secrets
   - Monitor logs for suspicious activity
   - Implement request signing

## Troubleshooting

### Cannot connect to MongoDB
- Ensure MongoDB is running: `mongod`
- Check connection string in .env
- Verify port 27017 is accessible

### SSH Connection Failed
- Test credentials manually: `ssh user@host`
- Check firewall allows port 22
- Verify username/password
- Try SSH key authentication

### API Not Responding
- Check backend is running: `npm run dev`
- Check port 5000 is not in use
- Check MongoDB connection
- Review backend logs

### Frontend Not Loading
- Check frontend is running: `npm start`
- Clear browser cache
- Check CORS_ORIGIN matches frontend URL
- Check browser console for errors

## Documentation

- [Getting Started Guide](docs/GETTING_STARTED.md) - Setup and first steps
- [SSH Integration Guide](docs/SSH_GUIDE.md) - SSH/SFTP usage and configuration
- [API Documentation](docs/API.md) - Complete API reference
- [Development Guide](docs/DEVELOPMENT.md) - Architecture and development

## Future Enhancements

- [ ] WebSocket for real-time console
- [ ] Docker container management
- [ ] Database management UI
- [ ] Backup scheduler
- [ ] Email notifications
- [ ] Two-factor authentication
- [ ] LDAP/OAuth integration
- [ ] Advanced analytics
- [ ] Mobile app

## License

MIT License - feel free to use for personal or commercial projects

## Support

For issues, feature requests, or contributions:
- Open a GitHub issue
- Check existing documentation
- Review SSH_GUIDE.md for SSH-related issues

## Contributors

Your contributions are welcome! Please:
1. Fork the repository
2. Create a feature branch
3. Commit your changes
4. Push to the branch
5. Open a pull request

