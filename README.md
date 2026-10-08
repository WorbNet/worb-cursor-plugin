
# Worb for Cursor

Connect Cursor to your Worb account and interact with your data through
the Worb MCP server.

## Features

- Connect using your own Worb account.
- Authenticate securely through OAuth.
- Read your own Worb profile.
- Update supported profile fields.
- Use Worb from compatible Cursor projects.

## Requirements

- Cursor with support for MCP servers and plugins.
- An active Worb account.
- Internet access to reach the Worb MCP server.

## Connection

Worb uses the hosted MCP server:

https://app.worb.net/mcp

Authentication is handled through Worb OAuth. Each user must authorize
their own account.

## Installation

This plugin is being prepared for distribution through GitHub and the
Cursor Marketplace.

Once published, install Worb from the Cursor Marketplace and follow
the authentication prompt to connect your Worb account.

## Available operations

- `get_my_profile`: retrieve the authenticated user's profile.
- `update_my_profile`: update supported fields in that profile.

Available operations depend on the tools exposed by the Worb MCP server.

## Security

- Never share your Worb password or access tokens.
- Each user accesses their own account through OAuth.
- Access permissions are enforced by the Worb server.
- Do not store private credentials in this repository.

## Support

Website: https://app.worb.net