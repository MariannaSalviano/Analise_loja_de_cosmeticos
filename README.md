# 📊 Análise de Vendas Loja de Cosméticos com MySQL

A base de dados utilizada neste projeto é fictícia, elaborada exclusivamente para fins de portfólio. Ela simula o histórico de vendas de uma empresa do segmento de cosméticos.

Este projeto tem por objetivo ...

---

## 🧱 Estrutura da Base de Dados
```sql
CREATE SCHEMA projeto_loja_cosmeticos;
USE projeto_loja_cosmeticos;
```

### 🗃️ Tabela: `Produtos`
```sql
CREATE TABLE produtos (
    id_produto INT NOT NULL AUTO_INCREMENT,
    nome_produto VARCHAR(150) NOT NULL,
    categoria VARCHAR(100) NOT NULL,
    marca VARCHAR(100) NOT NULL,
    preco_unitario DECIMAL(10,2) NOT NULL,
    data_cadastro DATE NOT NULL,
    PRIMARY KEY (id_produto)
);
```

### 👩‍💼 Tabela: `Vendedores`
```sql
CREATE TABLE vendedores (
    id_vendedor INT NOT NULL AUTO_INCREMENT,
    nome_vendedor VARCHAR(150) NOT NULL,
    data_contratacao DATE NOT NULL,
    ativo TINYINT(1) NOT NULL DEFAULT 1,
    PRIMARY KEY (id_vendedor)
);
```

### 📦 Tabela: `Estoque`
```sql
CREATE TABLE estoque (
    id_estoque INT NOT NULL AUTO_INCREMENT,
    id_produto INT NOT NULL,
    quantidade_disponivel INT NOT NULL,
    data_atualizacao DATETIME NOT NULL DEFAULT CURRENT_TIMESTAMP,
    PRIMARY KEY (id_estoque),
    FOREIGN KEY (id_produto) REFERENCES produtos(id_produto)
);
```

### 🛒 Tabela: `Vendas`
```sql
CREATE TABLE vendas (
    id_venda INT NOT NULL AUTO_INCREMENT,
    id_produto INT NOT NULL,
    id_vendedor INT NOT NULL,
    quantidade INT NOT NULL,
    valor_unitario DECIMAL(10,2) NOT NULL,
    valor_total DECIMAL(10,2) NOT NULL,
    data_venda DATE NOT NULL,
    PRIMARY KEY (id_venda)
);
```

```sql
-- Criando o relacionamento entre as tabelas
ALTER TABLE estoque 
ADD CONSTRAINT CE_estoque_produtos
FOREIGN KEY (id_produto)
REFERENCES produtos(id_produto)
ON DELETE NO ACTION
ON UPDATE NO ACTION;
```
```sql
-- Inserindo dados na tabela produtos
INSERT INTO produtos (id_produto, nome_produto, categoria, marca, preco_unitario, data_cadastro) VALUES
(1, 'Creme Facial Hidratante LuminaSoft 50ml', 'Skincare', 'BelleAura', 59.90, '2023-01-10'),
(2, 'Sérum Anti-Idade RadiantLift 30ml', 'Skincare', 'AuraVitta', 89.50, '2023-01-12'),
(3, 'Gel de Limpeza PurifySkin 120ml', 'Skincare', 'NovaDerma', 39.90, '2023-02-01'),
(4, 'Tônico Revitalizante SkinBoost 200ml', 'Skincare', 'DermaFlora', 44.90, '2023-02-05'),
(5, 'Protetor Solar FPS 50 SunGuard 60ml', 'Skincare', 'SolarisCare', 79.90, '2023-02-10'),
(6, 'Base Líquida VelvetTouch 30ml', 'Maquiagem', 'MakeVibe', 69.90, '2023-03-01'),
(7, 'Pó Compacto MatteSkin 10g', 'Maquiagem', 'GlowBerry', 39.90, '2023-03-05'),
(8, 'Máscara de Cílios VolumeMax', 'Maquiagem', 'LashBliss', 49.90, '2023-03-10'),
(9, 'Batom Matte RedBliss', 'Maquiagem', 'ColorVitta', 29.90, '2023-03-15'),
(10, 'Paleta de Sombras ColorDream', 'Maquiagem', 'MakeVibe', 79.90, '2023-03-20'),
(11, 'Shampoo NutriHair 300ml', 'Cabelos', 'HairEssentia', 25.90, '2023-04-01'),
(12, 'Condicionador NutriHair 300ml', 'Cabelos', 'HairEssentia', 27.90, '2023-04-01'),
(13, 'Máscara Capilar RepairMask 250g', 'Cabelos', 'CapelliPlus', 39.90, '2023-04-05'),
(14, 'Óleo Capilar ShineOil 100ml', 'Cabelos', 'CapelliPlus', 49.90, '2023-04-08'),
(15, 'Leave-in Defrisante SmoothHair 200ml', 'Cabelos', 'NovaDerma', 34.90, '2023-04-12'),
(16, 'Perfume Aurora 100ml', 'Perfumaria', 'EssenzaFleur', 159.90, '2023-05-01'),
(17, 'Perfume UrbanNight 100ml', 'Perfumaria', 'LuxVerde', 179.90, '2023-05-05'),
(18, 'Body Splash FreshBloom 200ml', 'Perfumaria', 'BelleAura', 49.90, '2023-05-10'),
(19, 'Deo Colônia CrystalDay 90ml', 'Perfumaria', 'LumiScents', 69.90, '2023-05-12'),
(20, 'Kit Perfume + Creme SweetGarden', 'Perfumaria', 'EssenzaFleur', 129.90, '2023-05-15'),
(21, 'Sabonete Líquido SoftCare 250ml', 'Corpo & Banho', 'DermaFlora', 19.90, '2023-06-01'),
(22, 'Hidratante Corporal SilkBody 400ml', 'Corpo & Banho', 'BelleAura', 29.90, '2023-06-03'),
(23, 'Esfoliante Corporal GentleScrub 200ml', 'Corpo & Banho', 'AuraVitta', 34.90, '2023-06-07'),
(24, 'Óleo Corporal GoldSkin 120ml', 'Corpo & Banho', 'LumiScents', 39.90, '2023-06-12'),
(25, 'Creme para Mãos SoftHands 60g', 'Corpo & Banho', 'SoftDerm', 14.90, '2023-06-14'),
(26, 'Base Cushion PerfectSkin', 'Maquiagem', 'GlowBerry', 89.90, '2023-07-01'),
(27, 'Delineador BlackInk Precision', 'Maquiagem', 'LashBliss', 39.90, '2023-07-05'),
(28, 'Iluminador GlowShine', 'Maquiagem', 'ColorVitta', 49.90, '2023-07-10'),
(29, 'Blush RosePetal', 'Maquiagem', 'MakeVibe', 42.90, '2023-07-12'),
(30, 'Primer PoreLess', 'Maquiagem', 'NovaDerma', 54.90, '2023-07-15'),
(31, 'Shampoo Anticaspa ClearBalance 300ml', 'Cabelos', 'HairEssentia', 29.90, '2023-08-01'),
(32, 'Condicionador Anticaspa ClearBalance 300ml', 'Cabelos', 'HairEssentia', 31.90, '2023-08-01'),
(33, 'Spray Reparador InstantRepair 150ml', 'Cabelos', 'CapelliPlus', 44.90, '2023-08-05'),
(34, 'Creme de Pentear CurlDefine 300ml', 'Cabelos', 'HairEssentia', 32.90, '2023-08-10'),
(35, 'Ampola Capilar PowerDose', 'Cabelos', 'NovaDerma', 12.90, '2023-08-12'),
(36, 'Perfume SunsetBloom 100ml', 'Perfumaria', 'EssenzaFleur', 149.90, '2023-09-01'),
(37, 'Perfume DeepOcean 100ml', 'Perfumaria', 'LuxVerde', 169.90, '2023-09-05'),
(38, 'Body Splash SweetShine 200ml', 'Perfumaria', 'LumiScents', 44.90, '2023-09-10'),
(39, 'Deo Colônia MysticGarden 90ml', 'Perfumaria', 'BelleAura', 69.90, '2023-09-12'),
(40, 'Kit Perfume + Loção FlowerDream', 'Perfumaria', 'EssenzaFleur', 139.90, '2023-09-15'),
(41, 'Sabonete Líquido DetoxCare 250ml', 'Corpo & Banho', 'SoftDerm', 21.90, '2023-10-01'),
(42, 'Hidratante Corporal MegaMoist 400ml', 'Corpo & Banho', 'DermaFlora', 31.90, '2023-10-03'),
(43, 'Esfoliante Corporal PureScrub 200ml', 'Corpo & Banho', 'AuraVitta', 36.90, '2023-10-06'),
(44, 'Óleo Corporal VelvetOil 120ml', 'Corpo & Banho', 'BelleAura', 42.90, '2023-10-10'),
(45, 'Creme para Pés SoftFeet 80g', 'Corpo & Banho', 'SoftDerm', 16.90, '2023-10-14'),
(46, 'Base Mate UltraSkin 30ml', 'Maquiagem', 'MakeVibe', 74.90, '2023-11-01'),
(47, 'Corretivo FullCover 12ml', 'Maquiagem', 'GlowBerry', 29.90, '2023-11-03'),
(48, 'Batom Hidratante ShineLips', 'Maquiagem', 'ColorVitta', 27.90, '2023-11-06'),
(49, 'Máscara de Cílios LengthPro', 'Maquiagem', 'LashBliss', 54.90, '2023-11-10'),
(50, 'Primer GlowPrime', 'Maquiagem', 'NovaDerma', 52.90, '2023-11-12'),
(51, 'Shampoo NutriCurl 300ml', 'Cabelos', 'HairEssentia', 27.90, '2023-12-01'),
(52, 'Condicionador NutriCurl 300ml', 'Cabelos', 'HairEssentia', 29.90, '2023-12-01'),
(53, 'Máscara Capilar NutriCurl 250g', 'Cabelos', 'CapelliPlus', 39.90, '2023-12-05'),
(54, 'Óleo Capilar NutriCurl Shine 100ml', 'Cabelos', 'CapelliPlus', 47.90, '2023-12-08'),
(55, 'Leave-in CurlBoost 200ml', 'Cabelos', 'NovaDerma', 35.90, '2023-12-12'),
(56, 'Perfume RoseElegance 100ml', 'Perfumaria', 'EssenzaFleur', 159.90, '2024-01-03'),
(57, 'Perfume BlueStorm 100ml', 'Perfumaria', 'LuxVerde', 189.90, '2024-01-05'),
(58, 'Body Splash CitrusDay 200ml', 'Perfumaria', 'BelleAura', 49.90, '2024-01-10'),
(59, 'Deo Colônia StarBloom 90ml', 'Perfumaria', 'LumiScents', 72.90, '2024-01-15'),
(60, 'Kit Perfume + Creme GoldSecret', 'Perfumaria', 'EssenzaFleur', 139.90, '2024-01-20'),
(61, 'Sabonete Líquido SensyCare 250ml', 'Corpo & Banho', 'SoftDerm', 22.90, '2024-02-01'),
(62, 'Hidratante Corporal DeepHydra 400ml', 'Corpo & Banho', 'BelleAura', 33.90, '2024-02-05'),
(63, 'Esfoliante Corporal OceanScrub 200ml', 'Corpo & Banho', 'DermaFlora', 37.90, '2024-02-08'),
(64, 'Óleo Corporal BlossomOil 120ml', 'Corpo & Banho', 'AuraVitta', 43.90, '2024-02-12'),
(65, 'Creme para Mãos RosaHydra 60g', 'Corpo & Banho', 'SoftDerm', 15.90, '2024-02-15'),
(66, 'Base Matte SuperCover', 'Maquiagem', 'GlowBerry', 79.90, '2024-03-01'),
(67, 'Delineador UltraBlack Pen', 'Maquiagem', 'LashBliss', 41.90, '2024-03-05'),
(68, 'Iluminador PearlGlow', 'Maquiagem', 'ColorVitta', 52.90, '2024-03-10'),
(69, 'Blush CoralDream', 'Maquiagem', 'MakeVibe', 45.90, '2024-03-12'),
(70, 'Primer MatteControl', 'Maquiagem', 'NovaDerma', 58.90, '2024-03-15'),
(71, 'Shampoo ControlOil 300ml', 'Cabelos', 'HairEssentia', 28.90, '2024-04-01'),
(72, 'Condicionador ControlOil 300ml', 'Cabelos', 'HairEssentia', 30.90, '2024-04-01'),
(73, 'Spray Reparador KeratinFix 150ml', 'Cabelos', 'CapelliPlus', 46.90, '2024-04-05'),
(74, 'Creme de Pentear Hydracurl 300ml', 'Cabelos', 'HairEssentia', 33.90, '2024-04-10'),
(75, 'Ampola Capilar NutriBoost', 'Cabelos', 'NovaDerma', 13.90, '2024-04-12'),
(76, 'Perfume SilverMoon 100ml', 'Perfumaria', 'EssenzaFleur', 169.90, '2024-05-01'),
(77, 'Perfume GreenForest 100ml', 'Perfumaria', 'LuxVerde', 179.90, '2024-05-05'),
(78, 'Body Splash FloralSky 200ml', 'Perfumaria', 'LumiScents', 46.90, '2024-05-10'),
(79, 'Deo Colônia PureSoul 90ml', 'Perfumaria', 'BelleAura', 74.90, '2024-05-12'),
(80, 'Kit Perfume + Loção BlossomDream', 'Perfumaria', 'EssenzaFleur', 149.90, '2024-05-15'),
(81, 'Sabonete Líquido SoftBerry 250ml', 'Corpo & Banho', 'DermaFlora', 23.90, '2024-06-01'),
(82, 'Hidratante Corporal VanillaSoft 400ml', 'Corpo & Banho', 'SoftDerm', 34.90, '2024-06-04'),
(83, 'Esfoliante Corporal SugarTouch 200ml', 'Corpo & Banho', 'BelleAura', 39.90, '2024-06-08'),
(84, 'Óleo Corporal MagicOil 120ml', 'Corpo & Banho', 'AuraVitta', 44.90, '2024-06-10'),
(85, 'Creme para Pés UltraCare 80g', 'Corpo & Banho', 'SoftDerm', 17.90, '2024-06-14'),
(86, 'Base Líquida HD PerfectSkin 30ml', 'Maquiagem', 'MakeVibe', 84.90, '2024-07-01'),
(87, 'Corretivo SkinMatch 12ml', 'Maquiagem', 'GlowBerry', 33.90, '2024-07-03'),
(88, 'Batom Matte ForeverRed', 'Maquiagem', 'ColorVitta', 32.90, '2024-07-06'),
(89, 'Máscara de Cílios ExtremeLift', 'Maquiagem', 'LashBliss', 59.90, '2024-07-10'),
(90, 'Primer SkinBlur', 'Maquiagem', 'NovaDerma', 63.90, '2024-07-12'),
(91, 'Shampoo UltraShine 300ml', 'Cabelos', 'HairEssentia', 29.90, '2024-08-01'),
(92, 'Condicionador UltraShine 300ml', 'Cabelos', 'HairEssentia', 31.90, '2024-08-01'),
(93, 'Máscara Capilar UltraShine 250g', 'Cabelos', 'CapelliPlus', 42.90, '2024-08-05'),
(94, 'Óleo Capilar UltraShine 100ml', 'Cabelos', 'CapelliPlus', 52.90, '2024-08-08'),
(95, 'Leave-in UltraRepair 200ml', 'Cabelos', 'NovaDerma', 36.90, '2024-08-12'),
(96, 'Perfume DreamLight 100ml', 'Perfumaria', 'EssenzaFleur', 179.90, '2024-09-01'),
(97, 'Perfume ForestNight 100ml', 'Perfumaria', 'LuxVerde', 189.90, '2024-09-05'),
(98, 'Body Splash OceanMist 200ml', 'Perfumaria', 'BelleAura', 51.90, '2024-09-10'),
(99, 'Deo Colônia PureMagic 90ml', 'Perfumaria', 'LumiScents', 78.90, '2024-09-12'),
(100, 'Kit Perfume + Creme InfinityLove', 'Perfumaria', 'EssenzaFleur', 159.90, '2024-09-15');
```
```sql
-- Inserindo dados na tabela estoque
INSERT INTO estoque (id_estoque, id_produto, quantidade_disponivel, data_atualizacao) VALUES
(1, 1, 347, '2024-12-31 23:59:59'),
(2, 2, 221, '2024-12-31 23:59:59'),
(3, 3, 492, '2024-12-31 23:59:59'),
(4, 4, 301, '2024-12-31 23:59:59'),
(5, 5, 155, '2024-12-31 23:59:59'),
(6, 6, 441, '2024-12-31 23:59:59'),
(7, 7, 289, '2024-12-31 23:59:59'),
(8, 8, 78, '2024-12-31 23:59:59'),
(9, 9, 196, '2024-12-31 23:59:59'),
(10, 10, 341, '2024-12-31 23:59:59'),
(11, 11, 143, '2024-12-31 23:59:59'),
(12, 12, 482, '2024-12-31 23:59:59'),
(13, 13, 117, '2024-12-31 23:59:59'),
(14, 14, 368, '2024-12-31 23:59:59'),
(15, 15, 420, '2024-12-31 23:59:59'),
(16, 16, 292, '2024-12-31 23:59:59'),
(17, 17, 474, '2024-12-31 23:59:59'),
(18, 18, 251, '2024-12-31 23:59:59'),
(19, 19, 133, '2024-12-31 23:59:59'),
(20, 20, 354, '2024-12-31 23:59:59'),
(21, 21, 498, '2024-12-31 23:59:59'),
(22, 22, 276, '2024-12-31 23:59:59'),
(23, 23, 61, '2024-12-31 23:59:59'),
(24, 24, 420, '2024-12-31 23:59:59'),
(25, 25, 159, '2024-12-31 23:59:59'),
(26, 26, 341, '2024-12-31 23:59:59'),
(27, 27, 212, '2024-12-31 23:59:59'),
(28, 28, 499, '2024-12-31 23:59:59'),
(29, 29, 64, '2024-12-31 23:59:59'),
(30, 30, 257, '2024-12-31 23:59:59'),
(31, 31, 344, '2024-12-31 23:59:59'),
(32, 32, 401, '2024-12-31 23:59:59'),
(33, 33, 159, '2024-12-31 23:59:59'),
(34, 34, 368, '2024-12-31 23:59:59'),
(35, 35, 284, '2024-12-31 23:59:59'),
(36, 36, 322, '2024-12-31 23:59:59'),
(37, 37, 151, '2024-12-31 23:59:59'),
(38, 38, 497, '2024-12-31 23:59:59'),
(39, 39, 433, '2024-12-31 23:59:59'),
(40, 40, 171, '2024-12-31 23:59:59'),
(41, 41, 260, '2024-12-31 23:59:59'),
(42, 42, 330, '2024-12-31 23:59:59'),
(43, 43, 446, '2024-12-31 23:59:59'),
(44, 44, 102, '2024-12-31 23:59:59'),
(45, 45, 492, '2024-12-31 23:59:59'),
(46, 46, 358, '2024-12-31 23:59:59'),
(47, 47, 245, '2024-12-31 23:59:59'),
(48, 48, 467, '2024-12-31 23:59:59'),
(49, 49, 189, '2024-12-31 23:59:59'),
(50, 50, 341, '2024-12-31 23:59:59'),
(51, 51, 474, '2024-12-31 23:59:59'),
(52, 52, 201, '2024-12-31 23:59:59'),
(53, 53, 49, '2024-12-31 23:59:59'),
(54, 54, 369, '2024-12-31 23:59:59'),
(55, 55, 260, '2024-12-31 23:59:59'),
(56, 56, 473, '2024-12-31 23:59:59'),
(57, 57, 94, '2024-12-31 23:59:59'),
(58, 58, 408, '2024-12-31 23:59:59'),
(59, 59, 175, '2024-12-31 23:59:59'),
(60, 60, 220, '2024-12-31 23:59:59'),
(61, 61, 396, '2024-12-31 23:59:59'),
(62, 62, 54, '2024-12-31 23:59:59'),
(63, 63, 311, '2024-12-31 23:59:59'),
(64, 64, 262, '2024-12-31 23:59:59'),
(65, 65, 497, '2024-12-31 23:59:59'),
(66, 66, 183, '2024-12-31 23:59:59'),
(67, 67, 424, '2024-12-31 23:59:59'),
(68, 68, 89, '2024-12-31 23:59:59'),
(69, 69, 140, '2024-12-31 23:59:59'),
(70, 70, 411, '2024-12-31 23:59:59'),
(71, 71, 254, '2024-12-31 23:59:59'),
(72, 72, 500, '2024-12-31 23:59:59'),
(73, 73, 337, '2024-12-31 23:59:59'),
(74, 74, 428, '2024-12-31 23:59:59'),
(75, 75, 142, '2024-12-31 23:59:59'),
(76, 76, 490, '2024-12-31 23:59:59'),
(77, 77, 219, '2024-12-31 23:59:59'),
(78, 78, 368, '2024-12-31 23:59:59'),
(79, 79, 192, '2024-12-31 23:59:59'),
(80, 80, 459, '2024-12-31 23:59:59'),
(81, 81, 441, '2024-12-31 23:59:59'),
(82, 82, 283, '2024-12-31 23:59:59'),
(83, 83, 179, '2024-12-31 23:59:59'),
(84, 84, 366, '2024-12-31 23:59:59'),
(85, 85, 257, '2024-12-31 23:59:59'),
(86, 86, 488, '2024-12-31 23:59:59'),
(87, 87, 67, '2024-12-31 23:59:59'),
(88, 88, 307, '2024-12-31 23:59:59'),
(89, 89, 381, '2024-12-31 23:59:59'),
(90, 90, 218, '2024-12-31 23:59:59'),
(91, 91, 499, '2024-12-31 23:59:59'),
(92, 92, 342, '2024-12-31 23:59:59'),
(93, 93, 270, '2024-12-31 23:59:59'),
(94, 94, 55, '2024-12-31 23:59:59'),
(95, 95, 367, '2024-12-31 23:59:59'),
(96, 96, 141, '2024-12-31 23:59:59'),
(97, 97, 482, '2024-12-31 23:59:59'),
(98, 98, 227, '2024-12-31 23:59:59'),
(99, 99, 304, '2024-12-31 23:59:59'),
(100, 100, 376, '2024-12-31 23:59:59');
```

```sql
-- Inserindo dados na tabela vendas
INSERT INTO vendas (id_venda, id_produto, id_vendedor, data_venda, quantidade, valor_unitario, valor_total) VALUES
(1, 4, 2, '2023-01-12', 3, 59.90, 179.70),
(2, 18, 5, '2023-02-08', 1, 129.50, 129.50),
(3, 33, 1, '2023-02-19', 2, 89.00, 178.00),
(4, 7, 10, '2023-03-03', 5, 42.75, 213.75),
(5, 52, 3, '2023-03-27', 2, 199.90, 399.80),
(6, 88, 7, '2023-04-11', 1, 349.00, 349.00),
(7, 14, 9, '2023-04-28', 4, 22.50, 90.00),
(8, 63, 6, '2023-05-06', 3, 119.00, 357.00),
(9, 25, 4, '2023-05-22', 2, 78.40, 156.80),
(10, 97, 1, '2023-06-01', 1, 450.00, 450.00),
(11, 41, 8, '2023-06-19', 6, 35.90, 215.40),
(12, 59, 2, '2023-07-04', 2, 149.90, 299.80),
(13, 80, 5, '2023-07-21', 3, 29.90, 89.70),
(14, 11, 7, '2023-08-09', 5, 65.00, 325.00),
(15, 100, 10, '2023-08-29', 1, 599.00, 599.00),
(16, 49, 4, '2023-09-07', 2, 134.50, 269.00),
(17, 27, 3, '2023-09-20', 3, 98.70, 296.10),
(18, 70, 6, '2023-10-04', 4, 45.20, 180.80),
(19, 55, 9, '2023-10-23', 2, 180.00, 360.00),
(20, 36, 1, '2023-11-02', 3, 310.00, 930.00),
(21, 3, 5, '2023-11-18', 1, 52.00, 52.00),
(22, 16, 8, '2023-12-01', 7, 18.50, 129.50),
(23, 72, 10, '2023-12-19', 2, 220.00, 440.00),
(24, 5, 4, '2024-01-06', 3, 65.90, 197.70),
(25, 23, 2, '2024-01-19', 1, 189.00, 189.00),
(26, 45, 7, '2024-02-02', 4, 36.90, 147.60),
(27, 60, 9, '2024-02-17', 2, 250.00, 500.00),
(28, 12, 3, '2024-03-08', 3, 72.00, 216.00),
(29, 84, 10, '2024-03-26', 1, 399.90, 399.90),
(30, 38, 6, '2024-04-10', 2, 111.00, 222.00),
(31, 95, 8, '2024-04-24', 1, 520.00, 520.00),
(32, 21, 5, '2024-05-03', 4, 28.50, 114.00),
(33, 67, 1, '2024-05-28', 2, 270.00, 540.00),
(34, 44, 4, '2024-06-11', 3, 49.90, 149.70),
(35, 9, 2, '2024-06-29', 5, 33.00, 165.00),
(36, 73, 7, '2024-07-09', 2, 189.50, 379.00),
(37, 57, 10, '2024-07-27', 1, 310.00, 310.00),
(38, 31, 6, '2024-08-05', 6, 15.90, 95.40),
(39, 91, 8, '2024-08-23', 2, 420.00, 840.00),
(40, 13, 3, '2024-09-10', 4, 75.00, 300.00),
(41, 50, 9, '2024-09-25', 3, 140.00, 420.00),
(42, 76, 1, '2024-10-04', 2, 260.00, 520.00),
(43, 28, 5, '2024-10-19', 1, 89.90, 89.90),
(44, 62, 4, '2024-11-02', 5, 39.50, 197.50),
(45, 48, 2, '2024-11-20', 2, 160.00, 320.00),
(46, 86, 7, '2024-12-03', 1, 580.00, 580.00),
(47, 19, 10, '2024-12-17', 3, 44.90, 134.70),
(48, 66, 6, '2024-12-29', 2, 205.00, 410.00),
(49, 1, 8, '2024-12-30', 4, 25.00, 100.00),
(50, 100, 9, '2024-12-31', 1, 599.00, 599.00);
```

```sql
-- Inserindo dados na tabela vendedores
INSERT INTO vendedores (id_vendedor, nome_vendedor, data_contratacao, ativo) VALUES
(1, 'Marina Duarte', '2022-01-10', 1),
(2, 'Carlos Menezes', '2022-03-15', 1),
(3, 'Juliana Rocha', '2022-05-20', 0),   -- Inativa
(4, 'Rafael Martins', '2022-08-02', 1),
(5, 'Bianca Salles', '2022-09-10', 1),
(6, 'Fernando Tavares', '2022-11-25', 0), -- Inativo
(7, 'Aline Albuquerque', '2023-01-05', 1),
(8, 'Lucas Monteiro', '2023-02-18', 1),
(9, 'Gabriela Farias', '2023-03-22', 1),
(10, 'Hugo Vasconcelos', '2023-04-10', 0), -- Inativo
(11, 'Patrícia Ribeiro', '2023-06-01', 1),
(12, 'Eduardo Silveira', '2023-07-09', 1),
(13, 'Mariana Couto', '2023-08-12', 1),
(14, 'Vinícius Prado', '2023-09-20', 1),
(15, 'Camila Teixeira', '2023-11-03', 0), -- Inativa
(16, 'Thiago Barbosa', '2024-01-10', 1),
(17, 'Larissa Carvalho', '2024-02-14', 1),
(18, 'Roberto Andrade', '2024-03-22', 1),
(19, 'Natália Moura', '2024-04-05', 1),
(20, 'Paulo Sérgio', '2024-05-10', 1);
```
---

## 📊 Consultas

```sql
SELECT id_produto, nome_produto, categoria, marca, preco_unitario
FROM produtos
WHERE categoria IN ('Skincare','Maquiagem') AND
marca NOT IN ('BelleAura', 'NovaDerma') 
AND preco_unitario > 52.90;
```

```sql
SELECT id_produto, nome_produto, categoria, marca, preco_unitario
FROM produtos
WHERE categoria IN ('Skincare','Maquiagem') AND 
marca IN ('BelleAura', 'NovaDerma') 
AND preco_unitario > 52.90;
```

```sql
SELECT DISTINCT id_produto, nome_produto, marca, data_cadastro FROM produtos
WHERE marca = ('NovaDerma') OR marca =('BelleAura')
ORDER BY data_cadastro DESC;

```sql
--Filtra os vendedores inativos
SELECT * FROM vendedores
WHERE ativo = 0;
```

```sql
--Filtra os vendedores ativos
SELECT * FROM vendedores
WHERE ativo = 1;
```

```sql
--Quantidade total de vendas por categoria
CREATE DEFINER=`root`@`localhost` PROCEDURE `quantidade_total_vendas_por_categoria`()
BEGIN
SELECT 
    p.categoria,
    SUM(v.quantidade) AS Qtd_total
FROM vendas AS v
INNER JOIN produtos AS p
    ON p.id_produto = v.id_produto
GROUP BY p.categoria
ORDER BY Qtd_total DESC;
END

CALL quantidade_total_vendas_por_categoria

```

```sql
--Quantidade total de vendas por vendedor
CREATE DEFINER=`root`@`localhost` PROCEDURE `quantidade_total_vendas`()
BEGIN
	SELECT vendas.id_vendedor, 
	vendedores.nome_vendedor, 
	SUM(vendas.quantidade) AS quantidade_total_vendas
	FROM vendas INNER JOIN vendedores
	ON vendas.id_vendedor = vendedores.id_vendedor
	GROUP BY vendas.ID_vendedor
	ORDER BY quantidade_total_vendas DESC;
END

CALL quantidade_total_vendas;
```

```sql
--Quantidade total de vendas por produto
CREATE DEFINER=`root`@`localhost` PROCEDURE `quantidade_total_vendas_por_produto`()
BEGIN
SELECT 
    v.id_produto,
    p.nome_produto,
    SUM(v.quantidade) AS Qtd_total
FROM vendas AS v
INNER JOIN produtos AS p
    ON p.id_produto = v.id_produto
GROUP BY v.id_produto, p.nome_produto
ORDER BY Qtd_total DESC;
END

CALL quantidade_total_vendas_por_produtos;
```

```sql
--Produtos com preço acima da média da categoria
SELECT 
    p.id_produto,
    p.nome_produto,
    p.categoria,
    p.preco_unitario
FROM produtos AS p
WHERE p.preco_unitario > (
    SELECT AVG(preco_unitario)
    FROM produtos
    WHERE categoria = p.categoria
);
```

```sql
--Top 5 produtos mais vendidos
SELECT
	p.id_produto,
    p.nome_produto,
    SUM(v.quantidade) AS total_vendas
FROM vendas AS v
INNER JOIN produtos AS p
    ON p.id_produto = v.id_produto
GROUP BY p.id_produto, p.nome_produto
ORDER BY total_vendas DESC
LIMIT 5;
```

```sql
--Produtos sem registro de vendas
SELECT 
    p.id_produto,
    p.nome_produto,
    p.categoria
FROM produtos AS p
LEFT JOIN vendas AS v
    ON v.id_produto = p.id_produto
WHERE v.id_produto IS NULL;
```
---

```sql
--Produtos mais caros por categoria
SELECT *
FROM produtos AS p
WHERE p.preco_unitario = (
    SELECT MAX(preco_unitario)
    FROM produtos
    WHERE categoria = p.categoria
);
```
---

```sql
--Total de vendas realizada por vendedor
SELECT 
    v.nome_vendedor,
    COALESCE(SUM(vd.valor_total), 0) AS valor_total_vendido
FROM vendedores v
LEFT JOIN vendas vd 
    ON vd.id_vendedor = v.id_vendedor
GROUP BY v.id_vendedor, v.nome_vendedor;
```
---

```sql
--Total de vendas realizada por vendedor com filtro
SELECT 
    v.nome_vendedor,
    COALESCE(SUM(vd.valor_total), 0) AS valor_total_vendido
FROM vendedores v
INNER JOIN vendas vd 
    ON vd.id_vendedor = v.id_vendedor
WHERE v.nome_vendedor IN ('Marina Duarte', 'Carlos Menezes')
GROUP BY v.id_vendedor, v.nome_vendedor;
```
---




