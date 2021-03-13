# leverage the work of Trinsic

Trinsic, for their studio, offers signup/login using verifiable credentials.
In their use case, the issuer and the verifier are identical.
But this is not necessary.

## for example, use Trinsic as a way to sign up for Manifold

We already allow a person to signup/login to Manifold using their
Google or GitHub accounts.

This idea is to use Trinsic as the issuer of a credential
(which of course they issue for their own purpose),
but to use that credential to create a Manifold account,
and later provide access to it.

So, Manifold becomes the verifier.

### the Trinsic credential
The Trinsic credential contains for a person who holds it:
1. the person's "Full Name" (as attested by the person themselves)
2. the person's "Account ID" (as assigned by Trinsic for their internal use)
3. the person's "Email" (attested by the person, but verified by Trinsic)

#### How this is useful for Manifold
Manifold gets owner information from either Google or GitHub currently,
and places it in the owner profile.

The numeric ID provided by Google or GitHub is used as the name of the owner pico.

We could use the Trinsic Account ID (a [GUID](https://en.wikipedia.org/wiki/Universally_unique_identifier)) 
as the name of the owner pico,
and put the Full Name and Email adress in the owner profile.

#### How it would work
To the existing Google and GitHub buttons we would add one for Trinsic.

Clicking on the Trinsic button would pop up a small window holding a QR Code
for a connectionless proof request.

When the owner (whether logging in or signing up for an account) scans
the QR Code with their Trinsic wallet, an Aries agent working on behalf of Manifold
would receive the requested proof.

If there is already an owner pico named by the "Account ID" then we will
log them in.
If not, we will create a manifold account for them and log them in.

### Artifacts

Starting with the QR Code Trinsic uses to request a proof,
`proof-request.png`
you can use [ZXing decoder](https://zxing.org/w/decode.jspx)
to find the `proof-request-url.txt`.

Using a browser to visit that URL, you will see the actual
out of band URL in your browser's location bar.
Captured here as `proof-request-oob-url.txt` for reference.

Taking the `dm` parameter, you can decode it using 
[https://www.base64decode.org/](https://www.base64decode.org/)
to get the DIDComm message, captured here as `proof-request.json`.
The structure of this is defined in [Aries RFC 0037](https://github.com/Picolab/aries-rfcs/tree/master/features/0037-present-proof).

One element of the request is also Base 64 encoded,
and the decoded value is here for reference as `proof-request-presentation.json`.
