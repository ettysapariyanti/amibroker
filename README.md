# amibroker
Penjelasan Mengenai Amibroker &amp; AFL


Tutorial dasar Amibroker:

[Amibroker Formula Language](https://enlightenedstocktrading.com/the-ultimate-free-amibroker-tutorial-guide/ "AFL")


Contoh source code AFL untuk menampilkan moving average:

```afl
// Downloaded From https://www.WiseStockTrader.com
_SECTION_BEGIN("Price");
SetChartOptions(0,chartShowArrows|chartShowDates);
_N(Title = StrFormat("{{NAME}} - {{INTERVAL}} {{DATE}} Open %g, Hi %g, Lo %g, Close %g (%.1f%%) {{VALUES}}", O, H, L, C, SelectedValue( ROC( C, 1 ) ) ));
Plot( C, "Close", ParamColor("Color", colorBlack ), styleNoTitle | ParamStyle("Style") | GetPriceStyle() ); 
_SECTION_END();
_SECTION_BEGIN("EMA");
P = ParamField("Price field",-1);
Periods1= Param("Periods1", 8, 2, 200, 1, 10 );
Plot( EMA  ( P, Periods1 ), _DEFAULT_NAME(), ParamColor( "Color", colorCycle ), ParamStyle("Style") ); 
_SECTION_END();

_SECTION_BEGIN("EMA1");
P = ParamField("Price field",-1);
Periods = Param("Periods", 13-10, 2, 200, 1, 10 );
Plot( EMA ( P, Periods ), _DEFAULT_NAME(), ParamColor( "Color", colorCycle ), ParamStyle("Style") ); 
_SECTION_END();
_SECTION_BEGIN("EMA2");
P = ParamField("Price field",-1);
Periods2 = Param("Periods2", 21-20, 2, 200, 1, 10 );
Plot( EMA ( P, Periods2 ), _DEFAULT_NAME(), ParamColor( "Color", colorCycle ), ParamStyle("Style") ); 
_SECTION_END();
Buy=Cross ( EMA(Close,Periods1), EMA(Close,Periods2) );
Sell = Cross( EMA(Close,Periods2), EMA(Close,Periods1) );
S = Sell;
B = Buy;
Shapes = ParamToggle("Plot Shapes","Off,On",1);
Buyshape = Param("Buy Shape Typ",1,0,50,1);
SellShape = Param("Sell Shape Typ",2,0,50,1);
Buyshapecolor = ParamColor("Buy Shape Color",colorBrightGreen);
Sellshapecolor = ParamColor("Sell Shape Color",colorRed);




PlotShapes(Buy*Buyshape*Shapes,Buyshapecolor,0,L,-15);
PlotShapes(Sell*Sellshape*Shapes,Sellshapecolor,0,H,-15);

AlertIf (S, "Sell", "Sell at: "+C+" Alert",0, 1+2+4+8,1 ); 
AlertIf (B, "Buy", "Buy at: "+C+" Alert",0, 1+2+4+8,1 );
 
PlotShapes((Buy*36)+(Sell*37),IIf(Buy,colorGreen,colorRed) );  
   


Filter = NOT GroupID()==253;
Filter = Filter AND (Buy OR Sell);


//AddColumn(Buy,"Rising wave start",1.0,colorBlack,IIf(Buy,colorPaleGreen,colorWhite),100);
//AddColumn(Buy,"Falling wave start",1.0,colorBlack,IIf(Sell,colorRose,colorWhite),100);
AddTextColumn(FullName(),"Full name");

```

Contoh source code AFL sederhana untuk bisa menampilkan tabel:

```c

//source code AFL custom

_SECTION_BEGIN("Menghitung Saham");

Plot(Close,"Candles",colorDefault,styleCandle);

// Plot(Close,"Candles",colorDefault);


_SECTION_END();


```

Penggabungan Moving Average 20 & Moving Average 50 :


```c

//source code AFL custom

_SECTION_BEGIN("Menghitung Saham");

// Plot(Close,"Candles",colorDefault,styleCandle);

// Plot(Close,"Candles",colorDefault);

Plot(Close,"Harga Penutupan",colorRed,styleCandle);

Plot(MA(Close,20),"Moving Average 20",colorGreen,styleLine | styleThick);

Plot(MA(Close,50),"Moving Average 50",colorBlue,styleLine | styleThick);


_SECTION_END();


```
