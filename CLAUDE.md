# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Overview

Minimal Express.js app that implements a WhatsApp webhook endpoint, deployed on Render. The entire application is a single file, `app.js`.

## Commands

- Install dependencies: `npm install` (or `yarn`, per README deploy instructions)
- Run the app: `npm start` (runs `node app.js`)
- No test suite, linter, or build step is currently configured.

## Architecture

- `app.js` is the whole app: an Express server with two routes on `/`.
  - `GET /` — WhatsApp webhook verification handshake. Checks `hub.mode` and `hub.verify_token` query params against the `VERIFY_TOKEN` env var and echoes back `hub.challenge` on success.
  - `POST /` — Webhook receiver. Logs the incoming payload (timestamp + JSON body) to the console; does not yet process or route message content.
- Configuration is via environment variables: `PORT` (default 3000) and `VERIFY_TOKEN` (used for webhook verification; requests are accepted unverified if unset).
- Deployment target is Render (see README.md for the deploy steps); the live instance is at https://express.onrender.com.
