# Mutex-vs-Monitor

공유 자원에 따른 lock 기법
- 공유 자원이 File 일 경우, (파일에 접근하는 스레드일 경우) rw.EnterWriteLock() / rw.ExitWriteLock()
- 공유 자원이 List, Array 같은 경우, mutex / Monitor
