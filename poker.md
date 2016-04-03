# poker-game
unit Unit1;

interface

uses
  Windows, Messages, SysUtils, Variants, Classes, Graphics, Controls, Forms,
  Dialogs, StdCtrls, ExtCtrls;

type
  TForm1 = class(TForm)
    Panel3: TPanel;
    Label13: TLabel;
    Label14: TLabel;
    Label15: TLabel;
    Label16: TLabel;
    Label17: TLabel;
    Label18: TLabel;
    RGNaipeCarta1Jogador1: TRadioGroup;
    RGNaipeCarta2Jogador1: TRadioGroup;
    RGNaipeCarta3Jogador1: TRadioGroup;
    RGNaipeCarta4Jogador1: TRadioGroup;
    RGNaipeCarta5Jogador1: TRadioGroup;
    CBCarta1Jogador1: TComboBox;
    CBCarta2Jogador1: TComboBox;
    CBCarta3Jogador1: TComboBox;
    CBCarta4Jogador1: TComboBox;
    CBCarta5Jogador1: TComboBox;
    Panel1: TPanel;
    Label1: TLabel;
    Label2: TLabel;
    Label3: TLabel;
    Label4: TLabel;
    Label5: TLabel;
    Label6: TLabel;
    RGNaipeCarta1Jogador2: TRadioGroup;
    RGNaipeCarta2Jogador2: TRadioGroup;
    RGNaipeCarta3Jogador2: TRadioGroup;
    RGNaipeCarta4Jogador2: TRadioGroup;
    RGNaipeCarta5Jogador2: TRadioGroup;
    CBCarta1Jogador2: TComboBox;
    CBCarta2Jogador2: TComboBox;
    CBCarta3Jogador2: TComboBox;
    CBCarta4Jogador2: TComboBox;
    CBCarta5Jogador2: TComboBox;
    Panel2: TPanel;
    Label7: TLabel;
    Button1: TButton;
    LbResultado: TLabel;
    procedure Button1Click(Sender: TObject);


  private
    { Private declarations }
  public
    { Public declarations }
  end;

var
  Form1: TForm1;
  Carta1J1 : Integer;
  Carta2J1 : Integer;
  Carta3J1 : Integer;
  Carta4J1 : Integer;
  Carta5J1 : Integer;
  Carta1J2 : Integer;
  Carta2J2 : Integer;
  Carta3J2 : Integer;
  Carta4J2 : Integer;
  Carta5J2 : Integer;
  NaipeC1J1 : Integer;
  NaipeC2J1 : Integer;
  NaipeC3J1 : Integer;
  NaipeC4J1 : Integer;
  NaipeC5J1 : Integer;
  NaipeC1J2 : Integer;
  NaipeC2J2 : Integer;
  NaipeC3J2 : Integer;
  NaipeC4J2 : Integer;
  NaipeC5J2 : Integer;

  i, j , k , l , max : Integer;
  CartaPar :Integer;
  maiorCartaPar :Integer;

  ArrayCartas : array[1..5] of integer;
  Arraytinca : array[1..9] of Boolean;
  ArrayPar : array[1..10] of Boolean;

  c1xc2 ,C1xC3, C1xC4 ,C1xC5, c2xC3, c2xC4, c2xC5, c3xc4, c3xc5, c4xc5: Boolean;
  c1xc2xc3, c1xc2xc4, c1xc2xc5, c1xc4xc5, c1xc3xc4, c1xc3xc5, c2xc3xc4, c2xc3xc5, c2xc4xc5, c3xc4xc5 : Boolean;

  seFlush : Boolean;
  sequadra : Boolean;
  seStraight : Boolean;
  seStraightFlush: Boolean;
  sePar : Boolean;
  seTrinca : Boolean;
  seRoyalFlush : Boolean;

  DoisPares : Integer;
     teste : integer;

implementation

{$R *.dfm}



procedure VerificaStraight(c1 , c2, c3, c4, c5: integer);
begin
    if(c5 = c4 + 1) and (c4 = c3 + 1) and (c3 = c2 + 1) and (c2 = c1 + 1) then
        seFlush := true
    else seFlush := false
end;

procedure VerificaStraightFlush(c1 , c2 , c3, c4, c5, n1, n2, n3, n4, n5: integer);
begin
    if((c5 = c4 + 1) and (c4 = c3 + 1) and (c3 = c2 + 1) and (c2 = c1 + 1)) and ((n1 = n2) and (n2 = n3) and (n3 = n4)and (n4 = n5)) then
        seStraightFlush := true
    else seStraightFlush := false
end;

procedure VerificaFlush( n1, n2, n3, n4, n5: integer);
begin
    if((n1 = n2) and (n2 = n3) and (n3 = n4)and (n4 = n5))then
        seFlush := true
    else seFlush := false
end;

procedure VerificaQuadra(c1 , c2, c3, c4, c5: integer);
begin
    if((c1 = c2) and (c2 = c3) and (c3 = c4)and (c4 = c5))then
        sequadra := true
    else sequadra := false
end;

Function VerificarCartasPar(c1 , c2: integer): Boolean;
begin
  if (c1 = c2)then
      Result := true
  else Result := false
end;

Function VerifiCartasTrinca(c1 , c2, c3: integer): Boolean;
begin
  if ((c1 = c2) and (c2 = c3))then
      Result := true
  else Result := false
end;

procedure VerificaPar();
begin
sePar := false;
j := 0;
ArrayPar[1] := c1xc2;
ArrayPar[2] := C1xC3;
ArrayPar[3] := C1xC4;
ArrayPar[4] := C1xC5;
ArrayPar[5] := c2xC3;
ArrayPar[6] := c2xC4;
ArrayPar[7] := c2xC5;
ArrayPar[8] := c3xc4;
ArrayPar[9] := c3xc5;
ArrayPar[10]:= c4xc5;

 for j := 1 to 10 do
         begin
         if(ArrayPar[j] = true)then
             sePar := true
         end;

	 j := j + 1;
end;

procedure VerificaDoisPares();
begin
DoisPares := 0;
l := 0;
ArrayPar[1] := c1xc2;
ArrayPar[2] := C1xC3;
ArrayPar[3] := C1xC4;
ArrayPar[4] := C1xC5;
ArrayPar[5] := c2xC3;
ArrayPar[6] := c2xC4;
ArrayPar[7] := c2xC5;
ArrayPar[8] := c3xc4;
ArrayPar[9] := c3xc5;
ArrayPar[10]:= c4xc5;

 for l := 1 to 10 do
         begin
         if(ArrayPar[l] = true)then
             DoisPares := DoisPares + 1;
         end;

	 l := l + 1;
end;


procedure verificaTrinca();
begin
seTrinca := false;
k := 0;
Arraytinca[1] := c1xc2xc3;
Arraytinca[2] := c1xc2xc4;
Arraytinca[3] := c1xc2xc5;
Arraytinca[4] := c1xc3xc4;
Arraytinca[5] := c1xc3xc5;
Arraytinca[6] := c2xc3xc4;
Arraytinca[7] := c2xc3xc5;
Arraytinca[8] := c2xc4xc5;
Arraytinca[9] := c3xc4xc5;


 for k := 1 to 9 do
         begin
         if(Arraytinca[k] = true)then
             seTrinca := true
         end;

	 k := k + 1;
end;

procedure Verificajogos(c1 , c2, c3, c4, c5: integer);
begin
c1xc2  := VerificarCartasPar(c1 , c2);
C1xC3  := VerificarCartasPar(c1 , c3);
C1xC4  := VerificarCartasPar(c1 , c4);
C1xC5  := VerificarCartasPar(c1 , c5);
c2xC3  := VerificarCartasPar(c2 , c3);
c2xC4  := VerificarCartasPar(c2 , c4);
c2xC5  := VerificarCartasPar(c2 , c5);
c3xc4  := VerificarCartasPar(c3 , c4);
c3xc5  := VerificarCartasPar(c3 , c5);
c4xc5  := VerificarCartasPar(c4 , c5);

c1xc2xc3 := VerifiCartasTrinca(C1, C2, C3);
c1xc2xc4 := VerifiCartasTrinca(C1, C2, C4);
c1xc2xc5 := VerifiCartasTrinca(C1, C2, C5);
c1xc3xc4 := VerifiCartasTrinca(C1, C3, C4);
c1xc3xc5 := VerifiCartasTrinca(C1, C4, C5);
c1xc4xc5 := VerifiCartasTrinca(C1, C4, C5);
c2xc3xc4 := VerifiCartasTrinca(C1, C3, C4);
c2xc3xc5 := VerifiCartasTrinca(C1, C3, C5);
c2xc4xc5 := VerifiCartasTrinca(C1, C4, C5);
c3xc4xc5 := VerifiCartasTrinca(C1, C4, C5);
VerificaPar();
VerificaDoisPares();
verificaTrinca();
end;

function verificaCartaMaior(c1 , c2 , c3, c4, c5: integer): integer;
begin
i   :=0;

    ArrayCartas[1] := c1;
    ArrayCartas[2] := c2;
    ArrayCartas[3] := c3;
    ArrayCartas[4] := c4;
    ArrayCartas[5] := c5;

   for i := 1 to 5 do
         begin
         if(ArrayCartas[i] > max)then
        		max := ArrayCartas[i];
     		 end;

	 i := i + 1;
   Result := max;
end;

procedure ValidaEntradaCartas(C1J1, C2J1, C3J1, C4J1, C5J1, C1J2, C2J2, C3J2, C4J2, C5J2 : Integer);
begin
   if (C1J1 = 0) or (C2J1 = 0) or (C3J1  = 0) or (C4J1  = 0)or (C5J1  = 0)or
      (C1J2 = 0) or (C2J2 = 0) or (C3J2  = 0) or (C4J2  = 0)or (C5J2  = 0)then
      ShowMessage('Informe todas as cartas')
end;


procedure VerificaRoyalFlush(C1, c2, c3, c4, c5: Integer);
begin
seRoyalFlush := false;
     if ((c1 = 9) and (c2 = 10) and (c3 = 11) and (c4 = 12) and (c5 = 13))then
       seRoyalFlush := true
end;

procedure ValidaEntradaNaipes(N1J1, N2J1, N3J1, N4J1, N5J1, N1J2, N2J2, N3J2, N4J2, N5J2 : Integer);
begin
   if (N1J1 = -1) or (N2J1 = -1) or (N3J1  = -1) or (N4J1  = -1)or (N5J1  = -1)or
      (N1J2 = -1) or (N2J2 = -1) or (N3J2  = -1) or (N4J2  = -1)or (N5J2  = -1)then
      ShowMessage('Informe todos os Nipes')
end;

function Pontuacao(c1 , c2 , c3, c4, c5, n1, n2, n3, n4, n5: integer): integer;
Var
resultado : integer;
begin
     Verificajogos(c1, c2, c3, c4, c5);
     VerificaFlush(n1, n2, n3, n4, n5);
     VerificaQuadra(c1, c2, c3, c4, c5);
     VerificaStraight(c1, c2, c3, c4, c5);
     VerificaStraightFlush(c1 , c2 , c3, c4, c5, n1, n2, n3, n4, n5);
     VerificaRoyalFlush(C1, c2, c3, c4, c5);

     if  (seRoyalFlush = true) then
             resultado := 1000
     else if (seStraightFlush = true)then
             resultado := 900
     else if (seQuadra = true)then
             resultado := 800
     //else if (seFullHouse = true)then
       //      resultado := 700
     else if (seflush = true)then
             resultado := 600
     else if (seStraight = true)then
             resultado := 500
     else if (seTrinca = true)then
             resultado := 400
     else if (doisPares = 2)then
             resultado := 300
     else if (separ = true)then
             resultado := 200
     else resultado :=  verificaCartaMaior(c1, c2, c3, c4, c5);

     Result := resultado;
end;

procedure TForm1.Button1Click(Sender: TObject);
begin
      Carta1J1 := CBCarta1Jogador1.ItemIndex;
      Carta2J1 := CBCarta2Jogador1.ItemIndex;
      Carta3J1 := CBCarta3Jogador1.ItemIndex;
      Carta4J1 := CBCarta4Jogador1.ItemIndex;
      Carta5J1 := CBCarta5Jogador1.ItemIndex;

      Carta1J2 := CBCarta1Jogador2.ItemIndex;
      Carta2J2 := CBCarta2Jogador2.ItemIndex;
      Carta3J2 := CBCarta3Jogador2.ItemIndex;
      Carta4J2 := CBCarta4Jogador2.ItemIndex;
      Carta5J2 := CBCarta5Jogador2.ItemIndex;

      NaipeC1J1 := RGNaipeCarta1Jogador1.ItemIndex;
      NaipeC2J1 := RGNaipeCarta2Jogador1.ItemIndex;
      NaipeC3J1 := RGNaipeCarta3Jogador1.ItemIndex;
      NaipeC4J1 := RGNaipeCarta4Jogador1.ItemIndex;
      NaipeC5J1 := RGNaipeCarta5Jogador1.ItemIndex;

      NaipeC1J2 := RGNaipeCarta1Jogador2.ItemIndex;
      NaipeC2J2 := RGNaipeCarta2Jogador2.ItemIndex;
      NaipeC3J2 := RGNaipeCarta3Jogador2.ItemIndex;
      NaipeC4J2 := RGNaipeCarta4Jogador2.ItemIndex;
      NaipeC5J2 := RGNaipeCarta5Jogador2.ItemIndex;



      ValidaEntradaCartas(Carta1J1, Carta2J1, Carta3J1, Carta4J1, Carta5J1, Carta1J2, Carta2J2, Carta3J2, Carta4J2, Carta5J2);
      ValidaEntradaNaipes(NaipeC1J1, NaipeC2J1, NaipeC3J1, NaipeC4J1, NaipeC5J1, NaipeC1J2, NaipeC2J2, NaipeC3J2, NaipeC4J2, NaipeC5J2);




if  (Pontuacao(Carta1J1, Carta2J1, Carta3J1, Carta4J1, Carta5J1, NaipeC1J1, NaipeC2J1, NaipeC3J1, NaipeC4J1, NaipeC5J1)
   > Pontuacao(Carta1J2, Carta2J2, Carta3J2, Carta4J2, Carta5J2, NaipeC1J2, NaipeC2J2, NaipeC3J2, NaipeC4J2, NaipeC5J2))then
          LbResultado.caption := 'Jogador 1 foi o vencedor'
else
          LbResultado.Caption := 'Jogador 2 foi o vencedor'
end;
end.

