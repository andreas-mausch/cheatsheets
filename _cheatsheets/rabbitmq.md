---
layout: cheatsheet
tags: messaging
logo: data:image/svg+xml;base64,PHN2ZyB3aWR0aD0iMjcxcHgiIGhlaWdodD0iMjcxcHgiIHZpZXdCb3g9Ii03LjUgMCAyNzEgMjcxIiB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHByZXNlcnZlQXNwZWN0UmF0aW89InhNaWRZTWlkIj48cGF0aCBkPSJNMjQ1LjQ0IDEwOC4zMDhoLTg1LjA5YTcuNzM4IDcuNzM4IDAgMCAxLTcuNzM1LTcuNzM0di04OC42OEMxNTIuNjE1IDUuMzI3IDE0Ny4yOSAwIDE0MC43MjYgMGgtMzAuMzc1Yy02LjU2OCAwLTExLjg5IDUuMzI3LTExLjg5IDExLjg5NHY4OC4xNDNjMCA0LjU3My0zLjY5NyA4LjI5LTguMjcgOC4zMWwtMjcuODg1LjEzM2MtNC42MTIuMDI1LTguMzU5LTMuNzE3LTguMzUtOC4zMjVsLjE3My04OC4yNDFDNTQuMTQ0IDUuMzM3IDQ4LjgxNyAwIDQyLjI0IDBIMTEuODlDNS4zMjEgMCAwIDUuMzI3IDAgMTEuODk0VjI2MC4yMWMwIDUuODM0IDQuNzI2IDEwLjU2IDEwLjU1NSAxMC41NkgyNDUuNDRjNS44MzQgMCAxMC41Ni00LjcyNiAxMC41Ni0xMC41NlYxMTguODY4YzAtNS44MzQtNC43MjYtMTAuNTYtMTAuNTYtMTAuNTZ6bS0zOS45MDIgOTMuMjMzYzAgNy42NDUtNi4xOTggMTMuODQ0LTEzLjg0MyAxMy44NDRIMTY3LjY5Yy03LjY0NiAwLTEzLjg0NC02LjE5OS0xMy44NDQtMTMuODQ0di0yNC4wMDVjMC03LjY0NiA2LjE5OC0xMy44NDQgMTMuODQ0LTEzLjg0NGgyNC4wMDVjNy42NDUgMCAxMy44NDMgNi4xOTggMTMuODQzIDEzLjg0NHYyNC4wMDV6IiBmaWxsPSIjRjYwIi8+PC9zdmc+
section:
  - name: Exchanges
    commands:
      Declare: rabbitmqadmin declare exchange name=my-exchange type=topic durable=true
      List: rabbitmqadmin list exchanges
  - name: Queues
    commands:
      Declare: rabbitmqadmin declare queue name=my-queue durable=true
      Declare with DLX: rabbitmqadmin declare queue name=my-queue-with-dlx durable=true arguments="{\"x-dead-letter-exchange\":\"dead-letter-exchange\"}"
      Declare quorum queue: rabbitmqadmin declare queue name=my-quorum-queue queue_type=quorum durable=true arguments="{\"x-dead-letter-exchange\":\"dead-letter-exchange\",\"x-delivery-limit\":3}"
      List: rabbitmqadmin list queues
  - name: Bindings
    commands:
      Bind exchange to queue: rabbitmqadmin declare binding source="my-exchange" destination_type="queue" destination="my-queue" routing_key="*"
  - name: Messages
    commands:
      Publish: rabbitmqadmin publish exchange=my-exchange routing_key=my-routing-key properties="{\"delivery_mode\":2}" payload='test'
      Get: rabbitmqadmin get queue=my-queue ackmode=ack_requeue_true --depth=4
  - name: Docker
    commands:
      run: docker run -it --name rabbitmq --rm -p 5672:5672 -p 15672:15672 rabbitmq:3.8-management
      rabbitmqadmin: docker exec -it rabbitmq rabbitmqadmin list exchanges
---

`durable` queues and exchanges survive a restart.

`delivery_mode` 2 means persistent message.
It only works with `durable` queues.

Possible values for `ackmode`:

| ackmode              | Description               |
|----------------------|---------------------------|
| ack_requeue_true     | Nack message requeue true |
| ack_requeue_false    | Automatic ack             |
| reject_requeue_true  | Reject requeue true       |
| reject_requeue_false | Reject requeue false      |

`--depth` is needed to display message headers.
