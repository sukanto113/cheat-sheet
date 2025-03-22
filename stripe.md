https://docs.stripe.com/stripe-cli

https://docs.stripe.com/webhooks


stripe listen --events checkout.session.completed,checkout.session.async_payment_succeeded,checkout.session.async_payment_failed --forward-to localhost:3000/stripe-webhook