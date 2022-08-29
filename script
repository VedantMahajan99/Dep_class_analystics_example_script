package com.nordstrom.allocation.platform.steps;
// Online Java Compiler
// Use this editor to write, compile and run your Java code online

import java.util.HashMap;

class test {

    public static void main(String[] args) {

        // -----------------------------------------------------SET FOLLOWING VARIABLES AS PER THE SCENARIO---------------------------------------------------------------
        int quantity_to_be_allocated = 200;
        int quantity_multiple = 5;

        int stockOnHand1 = 30, stockOnHand2 = 1 ,  stockOnHand3 = 8;
        int inTransitQty1 = 8, inTransitQty2 = 1, inTransitQty3 = 5;
        int tsfExpectedQty1 = 7, tsfExpectedQty2 = 1 , tsfExpectedQty3 = 5;
        int onOrderQty1 = 3, onOrderQty2 = 1 , onOrderQty3 = 2;
        int rtvQty1 = 8 , rtvQty2 = 1 , rtvQty3 = 7;
        int nonSellQty1 = 10, nonSellQty2 = 1, nonSellQty3 = 2;
        int tsfReservedQty1 = 5, tsfReservedQty2=1 , tsfReservedQty3 = 1;

        double ratio1 = .40, ratio2 = .30, ratio3 = .30;
        int location1 = 599, location2 = 584 , location3 = 568;
        //-----------------------------------------------------------------------------------------------------------------------------------------------------------------

        HashMap<Integer,Integer> available_inventory_quantity_map =  new HashMap<>();
        available_inventory_quantity_map.put(location1,availableInventory(stockOnHand1, inTransitQty1, tsfExpectedQty1 , onOrderQty1 , rtvQty1 ,nonSellQty1, tsfReservedQty1));
        available_inventory_quantity_map.put(location2,availableInventory(stockOnHand2, inTransitQty2, tsfExpectedQty2 , onOrderQty2 , rtvQty2 ,nonSellQty2, tsfReservedQty2));
        available_inventory_quantity_map.put(location3,availableInventory(stockOnHand3, inTransitQty3, tsfExpectedQty3 , onOrderQty3 , rtvQty3 ,nonSellQty3, tsfReservedQty3));

        int total_inventiry_quantity = 0;

        for(int key : available_inventory_quantity_map.keySet())
        {
            System.out.println("Location - "+ key + " available_inventory_quantity - " + available_inventory_quantity_map.get(key));
            total_inventiry_quantity += available_inventory_quantity_map.get(key);
        }

        System.out.println("total_inventiry_quantity - " + total_inventiry_quantity );

        int total_qty = total_inventiry_quantity + quantity_to_be_allocated;

        System.out.println("total_qty - " + total_qty );

        HashMap<Integer,Double> ratio_map = new HashMap<>();
        ratio_map.put(location1,ratio1);
        ratio_map.put(location2,ratio2);
        ratio_map.put(location3,ratio3);

        // STEP A

        System.out.println("\n\n STEP A \n\n");

        HashMap<Integer,Double> total_quantity_ratios_map = new HashMap<>();
        total_quantity_ratios_map.put(location1, total_qty*ratio_map.get(location1));
        total_quantity_ratios_map.put(location2, total_qty*ratio_map.get(location2));
        total_quantity_ratios_map.put(location3, total_qty*ratio_map.get(location3));

        for(int key : total_quantity_ratios_map.keySet())
        {
            System.out.println("Location - " + key + "  Qty - " + total_quantity_ratios_map.get(key));
        }

        //STEP B

        System.out.println("\n\n STEP B \n\n");

        HashMap<Integer,Double> subtract_available_inventory_map = new HashMap<>();
        subtract_available_inventory_map.put(location1, total_quantity_ratios_map.get(location1) - available_inventory_quantity_map.get(location1));
        subtract_available_inventory_map.put(location2, total_quantity_ratios_map.get(location2) - available_inventory_quantity_map.get(location2));
        subtract_available_inventory_map.put(location3, total_quantity_ratios_map.get(location3) - available_inventory_quantity_map.get(location3));

        for(int key : subtract_available_inventory_map.keySet())
        {
            System.out.println("Location - " + key + "  Qty - " + subtract_available_inventory_map.get(key));
        }

        double total_allocation_quantity = 0.0;

        for(int key : subtract_available_inventory_map.keySet())
        {
            total_allocation_quantity += subtract_available_inventory_map.get(key);
        }

        System.out.println("total_allocation_quantity - " + total_allocation_quantity );

        //STEP C

        System.out.println("\n\n STEP C \n\n");

        HashMap<Integer,Double> actual_split_quantity_map = new HashMap<>();
        actual_split_quantity_map.put(location1,(subtract_available_inventory_map.get(location1)/total_allocation_quantity)*quantity_to_be_allocated);
        actual_split_quantity_map.put(location2,(subtract_available_inventory_map.get(location2)/total_allocation_quantity)*quantity_to_be_allocated);
        actual_split_quantity_map.put(location3,(subtract_available_inventory_map.get(location3)/total_allocation_quantity)*quantity_to_be_allocated);

        for(int key : actual_split_quantity_map.keySet())
        {
            System.out.println("Location - " + key + "  Qty - " + actual_split_quantity_map.get(key));
        }

        //STEP D

        System.out.println("\n\n STEP D \n\n");

        HashMap<Integer,Integer> apply_order_quantitymultiple_map = new HashMap<>();
        apply_order_quantitymultiple_map.put(location1, ((int) Math.floor(actual_split_quantity_map.get(location1)/quantity_multiple)) *quantity_multiple);
        apply_order_quantitymultiple_map.put(location2, ((int) Math.floor(actual_split_quantity_map.get(location2)/quantity_multiple)) *quantity_multiple);
        apply_order_quantitymultiple_map.put(location3, ((int) Math.floor(actual_split_quantity_map.get(location3)/quantity_multiple)) *quantity_multiple);

        for(int key : apply_order_quantitymultiple_map.keySet())
        {
            System.out.println("Location - " + key + "  Qty - " + apply_order_quantitymultiple_map.get(key));
        }

        //STEP E

        System.out.println("\n\n STEP E \n\n");

        int remaining = 0;
        int allocated  = 0;

        for(int key : apply_order_quantitymultiple_map.keySet())
        {
            allocated += apply_order_quantitymultiple_map.get(key);
        }

        remaining = quantity_to_be_allocated - allocated;

        double maxratio = Math.max(ratio1,Math.max(ratio2,ratio3));

        int maxlocation = 0;

        for(int key : ratio_map.keySet())
        {
            if(ratio_map.get(key) == maxratio) maxlocation = key;
        }

        apply_order_quantitymultiple_map.put(maxlocation,apply_order_quantitymultiple_map.get(maxlocation)+remaining);

        // OUTPUT

        for(int key : apply_order_quantitymultiple_map.keySet())
        {
            System.out.println("Location - " + key + "  Qty - " + apply_order_quantitymultiple_map.get(key));
        }
    }

    public static int availableInventory(int stockOnHand, int inTransitQty , int tsfExpectedQty , int onOrderQty , int rtvQty , int nonSellQty, int tsfReservedQty  )
    {
        int calculatedInventoryQty =
                (stockOnHand + inTransitQty + tsfExpectedQty + onOrderQty)
                        - (rtvQty + nonSellQty + tsfReservedQty);

        return calculatedInventoryQty;
    }
}
