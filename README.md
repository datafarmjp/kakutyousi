# 課題
- FileMakerでオブジェクトフィールドにあるファイルの拡張子を知りたい

# 解決方法
- 以下のカスタム関数を作成
- 変数名は
	- object_file
	- file_name
- object_file、file_nameのどちらかを設定。使用しない方は""でOK。
- 両方入力されている場合はfile_nameが優先される

`Let ( `
`[`
	`dot = ".";`
	`filename=If(file_name="";GetAsText ( object_file );file_name);`
	`dotcount = PatternCount ( filename ; dot) ;`
	`dotstart = Position ( filename ; dot ; 0 ; dotcount ) +1;`
	`kakutyoushi_count = Length(filename)-dotstart+Length(dot)`
`] ;`
`Middle ( filename ; dotstart ; kakutyoushi_count )`
`)`

# 使用上の注意

- **オブジェクトフィールド（object_file）から直接取得する場合には、テーブルオカレンスも含んだフィールド名にする必要がある（オカレンス名::フィールド名）**

# ポイント
- ファイル名が入力済みのテキストフィールドがあれば、そこから拡張子を取得。
- 「.（ドット）」がいくつあっても正しくファイル名を取得できるように対応
