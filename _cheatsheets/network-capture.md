---
layout: cheatsheet
tags: wireshark termshark tcpdump pcap strace httptap
logo: data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHhtbG5zOnhsaW5rPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hsaW5rIiB3aWR0aD0iOTkuOTk2IiBoZWlnaHQ9Ijk5Ljg0MiIgdmVyc2lvbj0iMS4wIj48ZGVmcz48bGluZWFyR3JhZGllbnQgaWQ9ImMiPjxzdG9wIG9mZnNldD0iMCIgc3R5bGU9InN0b3AtY29sb3I6I2Q4ZDhkODtzdG9wLW9wYWNpdHk6LjgxOTY3MjExIi8+PHN0b3Agb2Zmc2V0PSIxIiBzdHlsZT0ic3RvcC1jb2xvcjojZmZmO3N0b3Atb3BhY2l0eTouMDEwOTI4OTYiLz48L2xpbmVhckdyYWRpZW50PjxsaW5lYXJHcmFkaWVudCBpZD0iYSI+PHN0b3Agb2Zmc2V0PSIwIiBzdHlsZT0ic3RvcC1jb2xvcjojNDBiMmU3O3N0b3Atb3BhY2l0eToxIi8+PHN0b3Agb2Zmc2V0PSIxIiBzdHlsZT0ic3RvcC1jb2xvcjojMTY3OWE3O3N0b3Atb3BhY2l0eTouOTM4MTQ0MzMiLz48L2xpbmVhckdyYWRpZW50PjxsaW5lYXJHcmFkaWVudCB4bGluazpocmVmPSIjYyIgaWQ9ImUiIHgxPSIxNzEuNDg2IiB4Mj0iMTcyLjA2OSIgeTE9IjI3OC43NTEiIHkyPSIyODkuODciIGdyYWRpZW50VHJhbnNmb3JtPSJtYXRyaXgoMS4wMDQ3IDAgMCAxLjMwNzcgLS42NzggLTg1LjczMykiIGdyYWRpZW50VW5pdHM9InVzZXJTcGFjZU9uVXNlIi8+PHJhZGlhbEdyYWRpZW50IHhsaW5rOmhyZWY9IiNhIiBpZD0iZCIgY3g9IjE4Ni44NjkiIGN5PSIzMTkuNjI1IiByPSI0OS45OTgiIGZ4PSIxODYuODY5IiBmeT0iMzE5LjYyNSIgZ3JhZGllbnRUcmFuc2Zvcm09Im1hdHJpeCgxIDAgMCAuOTk4NDYgMCAuNTAxKSIgZ3JhZGllbnRVbml0cz0idXNlclNwYWNlT25Vc2UiLz48L2RlZnM+PGcgdHJhbnNmb3JtPSJ0cmFuc2xhdGUoLTEzMy44NzcgLTI3NC42NDIpIj48cmVjdCB3aWR0aD0iOTUuNDQyIiBoZWlnaHQ9Ijk1LjI4OCIgeD0iMTM2LjE1NCIgeT0iMjc2LjkxOSIgcng9IjEwIiByeT0iMTAiIHN0eWxlPSJvcGFjaXR5OjE7ZmlsbDp1cmwoI2QpO2ZpbGwtb3BhY2l0eToxO3N0cm9rZTojMDAwO3N0cm9rZS13aWR0aDo0LjU1Mzk5OTk7c3Ryb2tlLWxpbmVqb2luOnJvdW5kO3N0cm9rZS1taXRlcmxpbWl0OjQ7c3Ryb2tlLWRhc2hhcnJheTpub25lO3N0cm9rZS1vcGFjaXR5OjEiLz48cGF0aCBkPSJNMTM2Ljg4IDM0Ny4zNjJoMjRzMy43ODQtNDguMTg4IDQ1Ljg1Mi00OC44NTFjLTEzLjU3IDIxLjIzOC0uODUyIDQ4Ljg1MS0uODUyIDQ4Ljg1MWgyNSIgc3R5bGU9ImZpbGw6bm9uZTtmaWxsLW9wYWNpdHk6Ljc1O2ZpbGwtcnVsZTpldmVub2RkO3N0cm9rZTojMDAwO3N0cm9rZS13aWR0aDo0LjI5NzIzNjkyO3N0cm9rZS1saW5lY2FwOmJ1dHQ7c3Ryb2tlLWxpbmVqb2luOnJvdW5kO3N0cm9rZS1taXRlcmxpbWl0OjQ7c3Ryb2tlLWRhc2hhcnJheTpub25lO3N0cm9rZS1vcGFjaXR5OjEiLz48cGF0aCBkPSJNMTQxIDI3Ny4zNjJjNy40MzQtMS41MTcgNzYuNDEtMiA4NSAwIDguMDMxIDEuODctMjIgMjgtNDIgMjhzLTUwLjU0Mi0yNi40Ni00My0yOCIgc3R5bGU9ImZpbGw6dXJsKCNlKTtmaWxsLW9wYWNpdHk6MTtzdHJva2U6bm9uZTtzdHJva2Utd2lkdGg6MDtzdHJva2UtbGluZWNhcDpyb3VuZDtzdHJva2UtbGluZWpvaW46cm91bmQ7c3Ryb2tlLW1pdGVybGltaXQ6NDtzdHJva2Utb3BhY2l0eToxIi8+PC9nPjwvc3ZnPg==
section:
  - name: Capture as PcapNg file
    commands:
      Capture network traffic of single process: sudo ptcpdump -w demo.pcapng -i any -- curl -L http://google.com
      Capture already running process (PID): sudo ptcpdump -w demo.pcapng -i any --pid 1234 -f
  - name: strace (log to stdout)
    commands:
      Capture network traffic of single process: strace -f -e trace=network -s 10000 curl -L http://google.com
      Capture already running process (PID): strace -f -e trace=network -s 10000 -p 1234
  - name: httptap
    commands:
      Capture: httptap -- curl https://andreas-mausch.de
  - name: Show open connections
    commands:
      - title: ss
        description: ss is a modern replacement for netstat
        command: sudo ss -tunap | sort -k1
        options:
          -t: "--tcp: Display TCP sockets."
          -u: "--udp: Display UDP sockets."
          -n: "--numeric: Do not try to resolve service names."
          -a: "--all: Display both listening and non-listening (for TCP this means established connections) sockets."
          -p: "--processes: Show process using socket."
---

<https://github.com/mozillazg/ptcpdump>
