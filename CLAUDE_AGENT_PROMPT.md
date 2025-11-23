# Citrus Admin Dashboard - AI Agent Instructions

## Project Overview
Admin dashboard for the Citrus receipt management platform. Provides admin tools for user management, system monitoring, and platform administration.

## Technology Stack
- **Framework**: React (check package.json)
- **Language**: TypeScript
- **Styling**: Tailwind CSS / CSS framework
- **Admin Features**: User management, analytics, settings
- **API**: Citrus backend endpoints

## Project Structure
```
citrus-admin-dashboard/
├── src/
│   ├── components/     # UI components
│   ├── pages/          # Admin pages
│   ├── api/            # API integration
│   ├── hooks/          # Custom React hooks
│   └── App.tsx         # Main application
├── public/             # Static assets
└── package.json        # Dependencies
```

## Development Guidelines

### Code Standards
1. **Admin Security**: Protect admin routes and actions
2. **Data Privacy**: Handle user data responsibly
3. **Error Handling**: Graceful error states
4. **Audit Logging**: Track admin actions where applicable
5. **Role-Based Access**: Respect permission levels

### Testing Your Changes
```bash
npm run build  # Must pass before completion
npm run dev    # Development server
```

### Branch Strategy
- **Main branch**: `main`
- **Agent branches**: `claude/agent-{NUMBER}-{description}`
- **Pull Requests**: Always create PRs to main

## Common Tasks

### Adding Admin Features
1. Create new page in `src/pages/`
2. Add route and navigation
3. Implement API integration
4. Add proper access controls
5. Test with different user roles

### User Management
1. CRUD operations for users
2. Role/permission management
3. Activity monitoring
4. Account controls

### Analytics & Reporting
1. Dashboard widgets
2. Data visualization
3. Export functionality
4. Real-time updates

## Important Notes
- This is admin dashboard only (separate from user-facing apps)
- Backend: Citrus backend API
- Security is paramount
- Test permission boundaries
- Related projects: citrus-developer-portal, citrus main apps

## Available Commands
Check `package.json` for scripts:
```bash
npm run dev     # Development server
npm run build   # Production build
npm run test    # Tests
```

## Current Priorities
1. Improve admin workflows
2. Add analytics features
3. Enhance user management
4. Optimize performance
5. Update documentation

## Security Checklist
- [ ] Admin routes protected
- [ ] API calls authenticated
- [ ] Sensitive data encrypted/masked
- [ ] Audit logs for critical actions
- [ ] Permission checks on all operations

---

**Last Updated**: 2025-11-19
**Maintained By**: Micro-Agent 001
