Trying to run a Quarto QMD document with both Python and Julia cells using https://github.com/PumasAI/QuartoNotebookRunner.jl.
Used as a reproducible example for https://github.com/PumasAI/QuartoNotebookRunner.jl/issues/276.

1. Install [pixi](https://pixi.sh/latest/)
1. Instantiate the julia environment.
1. Run `pixi run plot`
2. See if the line `plt.subplots()` produces the error below.

On Windows I get the following crash:

```
❯ pixi run plot
✨ Pixi task (plot): quarto render plot.qmd
Running [1/6] at line 5:  ENV["QUARTO_JULIA_PROJECT"]
Running [2/6] at line 9:  import PythonCall
Running [3/6] at line 14:  using CondaPkg
Running [4/6] at line 19:  CondaPkg.which("python")
Running [5/6] at line 23:  import sys
Running [6/6] at line 28:  import matplotlib.pyplot as plt
ERROR: Julia server returned error after receiving "run" command:
Failed to run notebook: C:\ProgramData\DevDrives\temp\c\plot.qmd
ERROR: QuartoNotebookRunner.Malt.TerminatedWorkerException()
Stacktrace:
  [1] unwrap_worker_result(worker::QuartoNotebookRunner.Malt.Worker, result::QuartoNotebookRunner.Malt.WorkerResult)
    @ QuartoNotebookRunner.Malt C:\ProgramData\DevDrives\.julia\packages\QuartoNotebookRunner\7Ikb9\src\Malt.jl:50
  [2] _wait_for_response(worker::QuartoNotebookRunner.Malt.Worker, msg_id::UInt64)
    @ QuartoNotebookRunner.Malt C:\ProgramData\DevDrives\.julia\packages\QuartoNotebookRunner\7Ikb9\src\Malt.jl:479
  [3] _send_receive
    @ C:\ProgramData\DevDrives\.julia\packages\QuartoNotebookRunner\7Ikb9\src\Malt.jl:490 [inlined]
  [4] #remote_call_fetch#22
    @ C:\ProgramData\DevDrives\.julia\packages\QuartoNotebookRunner\7Ikb9\src\Malt.jl:542 [inlined]
  [5] remote_call_fetch
    @ C:\ProgramData\DevDrives\.julia\packages\QuartoNotebookRunner\7Ikb9\src\Malt.jl:541 [inlined]
  [6] remote_eval_fetch
    @ C:\ProgramData\DevDrives\.julia\packages\QuartoNotebookRunner\7Ikb9\src\Malt.jl:613 [inlined]
  [7] remote_eval_fetch
    @ C:\ProgramData\DevDrives\.julia\packages\QuartoNotebookRunner\7Ikb9\src\Malt.jl:615 [inlined]
  [8] remote_eval_fetch_channeled(worker::QuartoNotebookRunner.Malt.Worker, expr::Expr)
    @ QuartoNotebookRunner C:\ProgramData\DevDrives\.julia\packages\QuartoNotebookRunner\7Ikb9\src\server.jl:161
  [9] macro expansion
    @ C:\ProgramData\DevDrives\.julia\packages\QuartoNotebookRunner\7Ikb9\src\server.jl:895 [inlined]
 [10] macro expansion
    @ C:\ProgramData\DevDrives\.julia\packages\ProgressLogging\6KXlp\src\ProgressLogging.jl:470 [inlined]
 [11] evaluate_raw_cells!(f::QuartoNotebookRunner.File, chunks::Vector{Any}, options::Dict{String, Any}; showprogress::Bool, chunk_callback::QuartoNotebookRunner.var"#chunk_callback#73"{TCPSocket})
    @ QuartoNotebookRunner C:\ProgramData\DevDrives\.julia\packages\QuartoNotebookRunner\7Ikb9\src\server.jl:801
 [12] evaluate!(f::QuartoNotebookRunner.File, output::Nothing; showprogress::Bool, options::Dict{String, Any}, chunk_callback::Function, markdown::String)
    @ QuartoNotebookRunner C:\ProgramData\DevDrives\.julia\packages\QuartoNotebookRunner\7Ikb9\src\server.jl:327
 [13] evaluate!
    @ C:\ProgramData\DevDrives\.julia\packages\QuartoNotebookRunner\7Ikb9\src\server.jl:267 [inlined]
 [14] (::QuartoNotebookRunner.var"#38#42"{Nothing, String, Bool, Dict{String, Any}, QuartoNotebookRunner.var"#chunk_callback#73"{TCPSocket}, Server})(file::QuartoNotebookRunner.File)
    @ QuartoNotebookRunner C:\ProgramData\DevDrives\.julia\packages\QuartoNotebookRunner\7Ikb9\src\server.jl:1433
 [15] (::QuartoNotebookRunner.var"#48#51"{Bool, QuartoNotebookRunner.var"#38#42"{Nothing, String, Bool, Dict{String, Any}, QuartoNotebookRunner.var"#chunk_callback#73"{TCPSocket}, Server}, Server, String})()
    @ QuartoNotebookRunner C:\ProgramData\DevDrives\.julia\packages\QuartoNotebookRunner\7Ikb9\src\server.jl:1505
 [16] lock(f::QuartoNotebookRunner.var"#48#51"{Bool, QuartoNotebookRunner.var"#38#42"{Nothing, String, Bool, Dict{String, Any}, QuartoNotebookRunner.var"#chunk_callback#73"{TCPSocket}, Server}, Server, String}, l::ReentrantLock)
    @ Base .\lock.jl:232
 [17] borrow_file!(f::QuartoNotebookRunner.var"#38#42"{Nothing, String, Bool, Dict{String, Any}, QuartoNotebookRunner.var"#chunk_callback#73"{TCPSocket}, Server}, server::Server, path::String; optionally_create::Bool, options::Dict{String, Any})
    @ QuartoNotebookRunner C:\ProgramData\DevDrives\.julia\packages\QuartoNotebookRunner\7Ikb9\src\server.jl:1498
 [18] borrow_file!
    @ C:\ProgramData\DevDrives\.julia\packages\QuartoNotebookRunner\7Ikb9\src\server.jl:1459 [inlined]
 [19] #run!#37
    @ C:\ProgramData\DevDrives\.julia\packages\QuartoNotebookRunner\7Ikb9\src\server.jl:1428 [inlined]
 [20] _handle_response_internal(socket::TCPSocket, notebooks::Server, request::@NamedTuple{type::String, content::Union{Dict{String, Any}, String}}, showprogress::Bool)
    @ QuartoNotebookRunner C:\ProgramData\DevDrives\.julia\packages\QuartoNotebookRunner\7Ikb9\src\socket.jl:314
 [21] _handle_response
    @ C:\ProgramData\DevDrives\.julia\packagERROR: Internal julia server error

Stack trace:
    at writeJuliaCommand (file:///C:/ProgramData/DevDrives/temp/c/.pixi/envs/default/Library/bin/quarto.js:41406:19)
    at eventLoopTick (ext:core/01_core.js:175:7)
    at async executeJulia (file:///C:/ProgramData/DevDrives/temp/c/.pixi/envs/default/Library/bin/quarto.js:41300:22)
    at async Object.execute (file:///C:/ProgramData/DevDrives/temp/c/.pixi/envs/default/Library/bin/quarto.js:41037:20)
    at async renderExecute (file:///C:/ProgramData/DevDrives/temp/c/.pixi/envs/default/Library/bin/quarto.js:85568:27)
    at async renderFileInternal (file:///C:/ProgramData/DevDrives/temp/c/.pixi/envs/default/Library/bin/quarto.js:85736:43)
    at async renderFiles (file:///C:/ProgramData/DevDrives/temp/c/.pixi/envs/default/Library/bin/quarto.js:85604:17)
    at async render (file:///C:/ProgramData/DevDrives/temp/c/.pixi/envs/default/Library/bin/quarto.js:90506:21)
    at async Command.actionHandler (file:///C:/ProgramData/DevDrives/temp/c/.pixi/envs/default/Library/bin/quarto.js:90654:32)
    at async Command.execute (file:///C:/ProgramData/DevDrives/temp/c/.pixi/envs/default/Library/bin/quarto.js:8111:13)
```
