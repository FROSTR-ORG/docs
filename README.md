# FROSTR

Simple t-of-n remote signing and key rotation protocol for nostr, using the powers of FROST.

This project was hacked together for entry in the TABCONF 2024 hack-a-thon event.

## Key Features

* Break up your secret key into decentralized, distributable shares.

* Sign messages using t-of-n signing devices (multiple devices available).

* If one share is compromised, your secret key is still safe.

* Discard and replace shares without changing your secret key (and identity).

## Architecture

`Bifrost :` FROST cryptography library.
`Igloo   :` Key management app & remote signing server.
`Frost2x :` Browser signing extension (forked from nos2x).

## How it Works

The protocol uses FROST in order to coordinate the signing of a message between multiple signing devices owned by a single user.

* Website makes a request to the user's signing device (to sign a note).

* User's device signs the note, then broadcasts a partial signature to the remote signing device(s).

* Each remote device verifies the signature and note, then returns their partial signature.

* User's device verifies each partial signature, combines them, and returns the complete signature to the website.

## Setting up your Devices

* Use Igloo to generate a set of FROST shares from your secret key.

* Import a share into Igloo to start the remote signing server.

* Import the remaining shares into your other devices.

* Cold-store the remaining shares for use in recovery.

## Rotating your Shares

* Collect together enough shares to meet your FROST threshold.

* Import the shares into Igloo's recovery page, then click "rotate" to produce a set of new shares.

* Import the new shares into each of your signing devices (including the remote signing server).

## Current Progress

* FROST library is complete, with unit tests and E2E tests.

* Igloo generates shares and runs a remote signing server.

* Frost2x extension signs via FROST and communicates with remote server.

* Remote server verifies, co-signs and returns a response.

## Unfinished Business

* Signing process needs to be debugged (invalid signatures).

* Key rotation needs to be implemented in igloo.

* Other signing methods need to be added (PSBT, ECDH, etc.).

## Resources

**Bifrost**  
Multi-platform Typescript FROST Library   
https://github.com/cmdruid/bifrost

**Igloo**  
Electron-based key-management app and remote signing server.  
https://github.com/TABCONF-2024-FROST/igloo

**Frost2x**  
Web extension signing device (fork of nos2x).  
https://github.com/TABCONF-2024-FROST/frost2x
