# cfs-flight-sw-lab

Laboratorio personal para aprender desarrollo de software de vuelo con NASA cFS:
compilar el core, arrancarlo, enviarle comandos y desarrollar apps propias.

## Entorno verificado

- Ubuntu 24.04.5 LTS en VirtualBox 7.0 (host Windows 11)
- cFS VERSION_AQUI, target `native_std`
- Evidencia del arranque: [`docs/arranque-native_std.log`](docs/arranque-native_std.log)
  (llega a `CFE_ES_Main entering OPERATIONAL state`)

## Compilar y arrancar

```bash
sudo apt install -y git build-essential cmake gdb cppcheck clang-tidy lcov \
  python3 python3-pip pkg-config liblua5.4-dev lua5.4 libjson-c-dev python3-dev
git clone --recurse-submodules https://github.com/nasa/cFS.git ~/cFS
cd ~/cFS
make native_std.prep
make native_std.install
sudo sysctl -w fs.mqueue.msg_max=256
cd build-native_std/exe/cpu1 && ./core-cpu1
```

## Problemas encontrados y soluciones

| Síntoma | Causa | Solución |
|---|---|---|
| `Unable to automatically determine the mission config directory` | Copié a mano `Makefile` y `sample_defs`, que ya vienen en la raíz | Restaurar con `git checkout` y no copiarlos |
| `Lua bindings are required to execute the EDS tool` | Faltaban `pkg-config` y Lua | `apt install pkg-config liblua5.4-dev lua5.4` |
| `i386-rtems5-gcc is not a full path...` | `make` sin target intenta compilar también RTEMS | Compilar solo `native_std.*` |

## Notas abiertas

- Durante el arranque aparecen avisos `Start/Stop FLYWHEEL` repetidos. Hipótesis
  (no comprobada): VirtualBox corre en modo NEM porque Windows tiene Hyper-V activo.
- Aviso `Pipe Overflow` en `DS_CMD_PIPE`: pendiente de investigar.

## Estructura del repo

- `docs/`: notas y evidencias
- `apps/`: apps cFS propias
- `lib/`: librerías propias# cfs-flight-sw-lab
