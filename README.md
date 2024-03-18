# 스레드 제어

공유 자원에 따른 lock 기법
- 공유 자원이 File 일 경우, (파일에 접근하는 스레드일 경우) rw.EnterWriteLock() / rw.ExitWriteLock()
- 공유 자원이 List, Array 같은 경우, mutex / Monitor

using 구문
- 명시적 Dispose 일 경우
  using (fileStream = new FileStream(path, FileMode.Append, FileAccess.Write, FileShare.ReadWrite))
  using (streamWriter = new StreamWriter(fileStream, Encoding.Default))
  try
  {
       rwLock.EnterWriteLock();
       try
       {
           streamWriter.WriteLine(Log[0]);
           Log.RemoveAt(0);
       }
       catch (Exception e)
       {
           Console.WriteLine("List Remove Error " + e);
       }
       finally
       {
           rwLock.ExitWriteLock();
       }
  }
  catch (Exception e)
  {
       Console.WriteLine("File Access Error\n" + e);
  }
  finally
  {
      streamWriter.Dispose();
      fileStream.Dispose();    // 이런 식으로 명시적으로 Dispose를 해줘야 한다.
  }

  - 명시적 Dispose가 아닌 경우
  using (fileStream = new FileStream(path, FileMode.Append, FileAccess.Write, FileShare.ReadWrite))
  using (streamWriter = new StreamWriter(fileStream, Encoding.Default)){      // 이런 식으로 객체가 사용되는 지점을 정해서 중괄호를 사용한다.
  try
  {
       rwLock.EnterWriteLock();
       try
       {
           streamWriter.WriteLine(Log[0]);
           Log.RemoveAt(0);
       }
       catch (Exception e)
       {
           Console.WriteLine("List Remove Error " + e);
       }
       finally
       {
           rwLock.ExitWriteLock();
       }
  }
  catch (Exception e)
  {
       Console.WriteLine("File Access Error\n" + e);
  }
  finally
  {
- }}
