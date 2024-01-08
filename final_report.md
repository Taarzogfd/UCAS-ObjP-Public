```c++
/// Preprocessor - This object engages in a tight little dance with the lexer to
/// efficiently preprocess tokens. 
///
class Preprocessor : public RefCountedBase<Preprocessor> {
  IntrusiveRefCntPtr<PreprocessorOptions> PPOpts;
  DiagnosticsEngine        *Diags;
  LangOptions       &LangOpts;
  const TargetInfo  *Target;
  FileManager       &FileMgr;
  SourceManager     &SourceMgr;
  ScratchBuffer     *ScratchBuf;
  HeaderSearch      &HeaderInfo;
  ModuleLoader      &TheModuleLoader;

  /// \brief External source of macros.
  ExternalPreprocessorSource *ExternalSource;


  /// PTH - An optional PTHManager object used for getting tokens from
  ///  a token cache rather than lexing the original source file.
  OwningPtr<PTHManager> PTH;
    
  ...
      
  /// CurLexer - This is the current top of the stack that we're lexing from if
  /// not expanding a macro and we are lexing directly from source code.
  ///  Only one of CurLexer, CurPTHLexer, or CurTokenLexer will be non-null.
  OwningPtr<Lexer> CurLexer;

  /// CurPTHLexer - This is the current top of stack that we're lexing from if
  ///  not expanding from a macro and we are lexing from a PTH cache.
  ///  Only one of CurLexer, CurPTHLexer, or CurTokenLexer will be non-null.
  OwningPtr<PTHLexer> CurPTHLexer;

  /// CurPPLexer - This is the current top of the stack what we're lexing from
  ///  if not expanding a macro.  This is an alias for either CurLexer or
  ///  CurPTHLexer.
  PreprocessorLexer *CurPPLexer;

  ...

}      
```

