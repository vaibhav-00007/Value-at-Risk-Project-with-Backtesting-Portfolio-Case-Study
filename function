// 1. Function to fetch Date + Close for any ticker
let
    fnGetStooq1Y = (Ticker as text) as table =>
    let
        // Download CSV
        Source = Csv.Document(
            Web.Contents("https://stooq.com/q/d/l/?s=" & Ticker & "&i=d"),
            [Delimiter=",", Columns=6, Encoding=65001, QuoteStyle=QuoteStyle.None]
        ),
        // Promote headers
        PromotedHeaders = Table.PromoteHeaders(Source, [PromoteAllScalars=true]),
        // Rename columns (English/Polish headers handled)
        RenamedColumns = Table.RenameColumns(PromotedHeaders, {
            {"Data", "Date"}, {"Zamkniecie", "Close"}
        }, MissingField.Ignore),
        // Keep only Date & Close
        KeptColumns = Table.SelectColumns(RenamedColumns, {"Date", "Close"}),
        // Change types
        ChangedType = Table.TransformColumnTypes(KeptColumns, {
            {"Date", type date}, {"Close", type number}
        }),
        // Filter last 1 year
        FilteredRows = Table.SelectRows(
            ChangedType,
            each [Date] >= Date.AddYears(Date.From(DateTime.LocalNow()), -1)
        )
    in
        FilteredRows
in
    fnGetStooq1Y
