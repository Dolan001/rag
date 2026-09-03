# Client experience contract

Build only PRD-required surfaces, commonly:

- knowledge-base/source list, upload validation, progress, ready/failed state, retry, replace, cancel,
  and delete confirmation;
- search or conversation with explicit sending, retrieving, generating, streaming, complete,
  cancelled, timeout, offline, rate-limited, provider-unavailable, and retry states;
- citations adjacent to claims, keyboard/screen-reader accessible source panels, page/section anchors,
  unavailable-source handling, and safe text rendering;
- conversation history, new-chat/reset behavior, copy/export policy, feedback with reason, and clear
  disclosure when an answer is grounded, partial, conflicting, or unsupported.

Do not render model HTML unsanitized. Treat citation metadata as untrusted, reject unsafe schemes,
and request source previews through authorized backend endpoints. Preserve the final answer and
citations across stream reconnect or HTTP recovery without duplicating tokens. Cancellation and
navigation must close transports and abort requests. Test keyboard navigation, focus announcements,
text scaling/zoom, reduced motion, long citations, slow networks, stream interruption, expired auth,
deleted sources, and mobile lifecycle restoration where applicable.

