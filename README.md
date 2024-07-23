# Federated Exchanges PoC

- Create two vhosts: `one` and `two`
- One vhost `one`, create an exchange called `one-source`
- `rabbitmqctl set_parameter federation-upstream origin '{"uri":"amqp://admin:admin@localhost:5672/one", "exchange":"one-source"}' --vhost two`
- `rabbitmqctl set_policy exchange-federation "^federated\." '{"federation-upstream-set":"all"}' --priority 10 --apply-to exchanges --vhost two`
- On vhost `two`, create one exchange called `federated.on-two`
- On vhost `two`, create a queue and bind it to the previously created exchange
- On vhost `one`, publish a message to the `one-source` exchange. It will be in ready state in the previously created queue on vhost `two`