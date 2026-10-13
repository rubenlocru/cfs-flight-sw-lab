# Primer comando: NOOP a cFE ES

Terminal A (core): `cd ~/cFS/build-native_std/exe/cpu1 && ./core-cpu1`

Terminal B: `./cmdUtil -v -ELE -A6 -C0` (APID 6 = ES, código 0 = NOOP, MID 0x1806)

Evento recibido:

    EVS Port1 ... 66/1/CFE_ES 3: No-op command:
     cFS Versions: cfe v7.0.1+dev1, osal v7.0.1+dev1, psp v7.0.1+dev1

Ciclo verificado: UDP 1234 -> CI_LAB -> cFE SB -> ES -> evento EVS.
